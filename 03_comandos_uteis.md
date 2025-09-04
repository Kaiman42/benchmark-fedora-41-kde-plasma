# Comandos Úteis

## Verificação de Hardware
```bash
# Verificar GPU em uso
glxinfo | grep "OpenGL renderer"

# Listar dispositivos PCI
lspci -k | grep -A 3 -i vga

# Verificar módulos carregados
lsmod | grep amd
```

## Gerenciamento de Energia
```bash
# Verificar perfil de energia atual
cat /sys/class/drm/card0/device/power_dpm_force_performance_level

# Alterar para modo de alto desempenho
echo high > /sys/class/drm/card0/device/power_dpm_force_performance_level
```

## Configuração de Drivers
```bash
# Instalar drivers Vulkan
sudo dnf5 install vulkan-loader vulkan-tools vulkan-loader.i686

# Instalar ferramentas de monitoramento
sudo dnf5 install radeon-profile

# Iniciar serviço de monitoramento
sudo systemctl start radeon-profile-daemon
sudo systemctl enable radeon-profile-daemon
```

## Configuração de Ambiente
```bash
# Forçar uso da GPU dedicada
export DRI_PRIME=0

# Configurar driver Vulkan
export VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/radeon_icd.x86_64.json

# Adicionar usuário ao grupo de vídeo
sudo usermod -a -G video $USER
```

### Helper no repositório
Há um script helper que facilita aplicar essas variáveis e testar controles de ventoinha via sysfs:

```bash
# Aplicar as variáveis na sessão atual (source):
source scripts/setup_gpu_env.sh

# Mostrar hwmon e sensores amdgpu
./scripts/setup_gpu_env.sh --show-hwmon

# Tentar aplicar PWM manual (150) — precisa de sudo
./scripts/setup_gpu_env.sh --apply-pwm 150

# Reverter pwm para controle automático
./scripts/setup_gpu_env.sh --revert-pwm
```

Consulte `scripts/setup_gpu_env.sh --help` para mais opções e avisos.

## Monitoramento
```bash
# Verificar uso da GPU
watch -n 1 "cat /sys/class/drm/card0/device/gpu_busy_percent"

# Verificar temperatura
watch -n 1 "cat /sys/class/drm/card0/device/hwmon/hwmon*/temp1_input"

# Verificar temperatura alternativo
sudo dnf5 install lm_sensors
sensors-detect --auto
sensors

# Verificar velocidade das ventoinhas
watch -n 1 "cat /sys/class/drm/card0/device/hwmon/hwmon*/fan1_input"
```

## Controle Manual das Ventoinhas
```bash
# Habilitar controle manual
echo 1 | sudo tee /sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_enable

# Verificar velocidade mínima e máxima
cat /sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_min
cat /sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_max

# Definir velocidade (0-255)
echo 150 | sudo tee /sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1

# Voltar para controle automático
echo 2 | sudo tee /sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_enable

# Monitorar temperatura em tempo real
watch -n 1 "cat /sys/class/drm/card0/device/hwmon/hwmon*/temp1_input"

# Verificar estado de energia DPM
cat /sys/class/drm/card0/device/power_dpm_state

# Verificar nível de desempenho forçado
cat /sys/class/drm/card0/device/power_dpm_force_performance_level
```

## Logs do Sistema
```bash
# Verificar logs do kernel para erros do AMDGPU
journalctl -k | grep -i amdgpu

# Verificar mensagens de inicialização do kernel
dmesg | grep -i amdgpu
```
