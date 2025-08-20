# Problemas e Soluções

## Problema 1: Ventoinhas da GPU não giram
- **Sintomas**: Ventoinhas da RX 7600 não giram, mesmo sob carga
- **Temperatura em repouso**: 30-31°C
- **Driver em uso**: amdgpu (open-source)

### Soluções Testadas

#### 1. Verificação de Drivers
- Verificado driver em uso: `amdgpu`
- Módulos carregados corretamente
- **Resultado**: Drivers OK, mas problema persiste

#### 2. Configuração de Energia
- Alterado perfil de energia para "high":
  ```bash
  echo high > /sys/class/drm/card0/device/power_dpm_force_performance_level
  ```
- **Resultado**: Sem alteração no comportamento das ventoinhas

#### 3. Instalação do Radeon Profile
- Instalado pacote `radeon-profile`
- Iniciado serviço:
  ```bash
  sudo systemctl start radeon-profile-daemon
  sudo systemctl enable radeon-profile-daemon
  ```
- **Resultado**: Em avaliação

#### 4. Configuração do GRUB
- Adicionados parâmetros ao kernel:
  ```
  amdgpu.ppfeaturemask=0xffffffff amdgpu.dpm=1 amdgpu.runpm=1
  ```
- **Resultado**: Problemas com o ambiente gráfico, revertido

## Problema 2: GPU Integrada vs Dedicada
- Sistema possui duas GPUs: 
  - Integrada: AMD Radeon Graphics (RENOIR)
  - Dedicada: AMD Radeon RX 7600 (NAVI33)

### Comportamento Atual
- Sem `DRI_PRIME`: Usa RX 7600
- Com `DRI_PRIME=1`: Muda para GPU integrada
- Com `DRI_PRIME=0`: Mantém na RX 7600

### Soluções em Teste
- Adicionado ao `.bashrc`:
  ```bash
  export DRI_PRIME=0
  export VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/radeon_icd.x86_64.json
  ```
- **Resultado**: Em avaliação

## Resultados dos Comandos de Diagnóstico

### 1. Verificação de Controle de Ventoinhas
- **Comando**: `ls -la /sys/class/drm/card0/device/hwmon/hwmon*/pwm*`
  - **Resultado**: `Arquivo ou diretório inexistente`
  - **Análise**: O sistema não está expondo os controles PWM das ventoinhas no caminho esperado

- **Tentativa de ativação manual**:
  ```bash
  echo 1 | sudo tee /sys/class/drm/card0/device/hwmon/hwmon*/pwm1_enable
  echo 150 | sudo tee /sys/class/drm/card0/device/hwmon/hwmon*/pwm1
  ```
  - **Resultado**: Falha - Arquivos não encontrados

### 2. Configurações de Energia
- **Estado DPM Atual**: `performance`
  ```bash
  cat /sys/class/drm/card0/device/power_dpm_state
  ```

- **Nível de Desempenho Forçado**: `auto`
  ```bash
  cat /sys/class/drm/card0/device/power_dpm_force_performance_level
  ```

## Análise dos Logs do Kernel
- **Overdrive ativado**: `amdgpu: Overdrive is enabled, please disable it before reporting any bugs unrelated to overdrive.`
- **SMU Inicializado com Sucesso**: `amdgpu: SMU is initialized successfully!`
- **Versão do Driver AMDGPU**: 3.63.0
- **VRAM Detectada**: 8176MB (RX 7600) e 512MB (GPU Integrada)
- **Problema de Timeout Detectado**: `REG_WAIT timeout 1us * 150000 tries - optc32_disable_crtc line:195`

## Descobertas Importantes

### 1. Arquivos de Controle de Ventoinha
Foram encontrados arquivos de controle PWM em:
```
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_enable
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_min
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_max
```

### 2. Atualizações Disponíveis
- Várias atualizações do KDE Plasma 6.4.3 disponíveis
- Nenhuma atualização do kernel ou drivers AMD disponível no momento

## Próximos Passos
1. Testar o controle manual das ventoinhas usando os arquivos encontrados
2. Verificar as permissões dos arquivos de controle
4. Monitorar as temperaturas após ajustes
