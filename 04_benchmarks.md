# Resultados de Benchmarks

## Teste de Desempenho com glxgears
```
300 frames in 5.0 seconds = 60.000 FPS
300 frames in 5.0 seconds = 59.987 FPS
300 frames in 5.0 seconds = 60.000 FPS
```
- **GPU em uso**: AMD Radeon RX 7600
- **Resolução**: 2560x1080
- **VSync**: Ativado (limite de 60 FPS)

## Teste com glmark2
```
=======================================================
    glmark2 2023.01
=======================================================
    OpenGL Information
    GL_VENDOR:      AMD
    GL_RENDERER:    AMD Radeon RX 7600 (radeonsi, navi33, LLVM 19.1.7, DRM 3.63, 6.15.6-100.fc41.x86_64)
    GL_VERSION:     4.6 (Compatibility Profile) Mesa 25.0.7
    Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
    Surface Size:   2560x1080 fullscreen
=======================================================
[build] use-vbo=false: FPS: 9036 FrameTime: 0.111 ms
=======================================================
                                  glmark2 Score: 9035 
```

## Uso de Recursos
- **Uso de VRAM em repouso**: 17MB de 487MB
- **Clock da Memória**: 1.60 GHz (100%)
- **Clock do Shader**: 0.40 GHz (21.05% do máximo de 1.90 GHz)
- **Temperatura em repouso**: 30-31°C

## Teste de Desempenho da CPU
```
analisando o CPU 5:
  driver: amd-pstate-epp
  energy performance preference: performance
  limites do hardware: 422 MHz - 4.67 GHz
  política de frequência atual: entre 2.39 GHz e 4.67 GHz
  current CPU frequency: 4.64 GHz (asserted by call to kernel)
  boost state support:
    Supported: yes
    Active: yes
  amd-pstate limits:
    Highest Performance: 166. Maximum Frequency: 4.67 GHz.
    Nominal Performance: 128. Nominal Frequency: 3.60 GHz.
    Lowest Non-linear Performance: 85. Lowest Non-linear Frequency: 2.39 GHz.
    Lowest Performance: 15. Lowest Frequency: 400 MHz.
```

## Estado Atual da GPU

### Parâmetros de Energia
- **Estado DPM Atual**: `performance`
- **Nível de Desempenho Forçado**: `auto`
- **Overdrive**: Ativado (pode causar instabilidades)
- **VRAM Total**: 8176MB (RX 7600) / 512MB (GPU Integrada)
- **Driver AMDGPU**: 3.63.0

### Controle de Ventoinhas
- **Status**: Controle manual não disponível via sysfs
- **Arquivos de Controle**: Não encontrados em `/sys/class/drm/card0/device/hwmon/`
- **Temperatura em Repouso**: ~30-31°C

## Observações
- A GPU está limitada pelo VSync a 60 FPS
- O clock da memória está em 100% mesmo em repouso, o que pode indicar um comportamento anômalo
- As ventoinhas não estão ativando automaticamente conforme a temperatura aumenta
- SMU (System Management Unit) inicializada com sucesso, mas com aviso de versão não correspondente
- Detectado problema de timeout no driver: `REG_WAIT timeout 1us * 150000 tries - optc32_disable_crtc line:195`

----------------------------------

esses pacotes são de uma atualização de versão do sistema, ou seja, o que significaria eu ir do 41 ao 42, o que eu quero evitar.

kaiman@kaiman:~$ sudo dnf5 check-update
[sudo] senha para kaiman: 
Atualizando e carregando repositórios:
Repositórios carregados.
aurorae.x86_64                         6.4.3-1.fc41   updates
bluedevil.x86_64                       6.4.3-1.fc41   updates
breeze-cursor-theme.noarch             6.4.3-1.fc41   updates
breeze-gtk-common.noarch               6.4.3-1.fc41   updates
breeze-gtk-gtk2.noarch                 6.4.3-1.fc41   updates
breeze-gtk-gtk3.noarch                 6.4.3-1.fc41   updates
breeze-gtk-gtk4.noarch                 6.4.3-1.fc41   updates
flatpak-kcm.x86_64                     6.4.3-1.fc41   updates
ibus-typing-booster.noarch             2.27.70-1.fc41 updates
kactivitymanagerd.x86_64               6.4.3-1.fc41   updates
kde-cli-tools.x86_64                   6.4.3-1.fc41   updates
kde-gtk-config.x86_64                  6.4.3-1.fc41   updates
kdecoration.x86_64                     6.4.3-1.fc41   updates
kdeplasma-addons.x86_64                6.4.3-1.fc41   updates
kdesu.x86_64                           1:6.4.3-1.fc41 updates
kglobalacceld.x86_64                   6.4.3-1.fc41   updates
kinfocenter.x86_64                     6.4.3-1.fc41   updates
kmenuedit.x86_64                       6.4.3-1.fc41   updates
kpipewire.x86_64                       6.4.3-1.fc41   updates
krdp.x86_64                            6.4.3-1.fc41   updates
krdp-libs.x86_64                       6.4.3-1.fc41   updates
kscreen.x86_64                         1:6.4.3-1.fc41 updates
kscreenlocker.x86_64                   6.4.3-1.fc41   updates
ksshaskpass.x86_64                     6.4.3-1.fc41   updates
ksystemstats.x86_64                    6.4.3-1.fc41   updates
kwayland.x86_64                        6.4.3-1.fc41   updates
kwayland-integration.x86_64            6.4.3-1.fc41   updates
kwin.x86_64                            6.4.3-1.fc41   updates
kwin-common.x86_64                     6.4.3-1.fc41   updates
kwin-libs.x86_64                       6.4.3-1.fc41   updates
kwrited.x86_64                         6.4.3-1.fc41   updates
langtable.noarch                       0.0.69-1.fc41  updates
layer-shell-qt.x86_64                  6.4.3-1.fc41   updates
libkscreen.x86_64                      6.4.3-1.fc41   updates
libksysguard.x86_64                    6.4.3-1.fc41   updates
libksysguard-common.x86_64             6.4.3-1.fc41   updates
libkworkspace6.x86_64                  6.4.3-1.fc41   updates
libplasma.x86_64                       6.4.3-1.fc41   updates
ocean-sound-theme.noarch               6.4.3-1.fc41   updates
pam-kwallet.x86_64                     6.4.3-1.fc41   updates
plasma-activities.x86_64               6.4.3-1.fc41   updates
plasma-activities-stats.x86_64         6.4.3-1.fc41   updates
plasma-breeze.x86_64                   6.4.3-1.fc41   updates
plasma-breeze-common.noarch            6.4.3-1.fc41   updates
plasma-breeze-qt5.x86_64               6.4.3-1.fc41   updates
plasma-breeze-qt6.x86_64               6.4.3-1.fc41   updates
plasma-browser-integration.x86_64      6.4.3-1.fc41   updates
plasma-desktop.x86_64                  6.4.3-1.fc41   updates
plasma-desktop-doc.noarch              6.4.3-1.fc41   updates
plasma-discover.x86_64                 6.4.3-1.fc41   updates
plasma-discover-flatpak.x86_64         6.4.3-1.fc41   updates
plasma-discover-kns.x86_64             6.4.3-1.fc41   updates
plasma-discover-libs.x86_64            6.4.3-1.fc41   updates
plasma-discover-notifier.x86_64        6.4.3-1.fc41   updates
plasma-discover-offline-updates.x86_64 6.4.3-1.fc41   updates
plasma-discover-packagekit.x86_64      6.4.3-1.fc41   updates
plasma-disks.x86_64                    6.4.3-1.fc41   updates
plasma-drkonqi.x86_64                  6.4.3-1.fc41   updates
plasma-integration.x86_64              6.4.3-1.fc41   updates
plasma-integration-qt5.x86_64          6.4.3-1.fc41   updates
plasma-lookandfeel-fedora.noarch       6.4.3-1.fc41   updates
plasma-milou.x86_64                    6.4.3-1.fc41   updates
plasma-nm.x86_64                       6.4.3-1.fc41   updates
plasma-nm-l2tp.x86_64                  6.4.3-1.fc41   updates
plasma-nm-openconnect.x86_64           6.4.3-1.fc41   updates
plasma-nm-openswan.x86_64              6.4.3-1.fc41   updates
plasma-nm-openvpn.x86_64               6.4.3-1.fc41   updates
plasma-nm-pptp.x86_64                  6.4.3-1.fc41   updates
plasma-nm-vpnc.x86_64                  6.4.3-1.fc41   updates
plasma-pa.x86_64                       6.4.3-1.fc41   updates
plasma-print-manager.x86_64            6.4.3-1.fc41   updates
plasma-print-manager-libs.x86_64       6.4.3-1.fc41   updates
plasma-systemmonitor.x86_64            6.4.3-1.fc41   updates
plasma-systemsettings.x86_64           6.4.3-1.fc41   updates
plasma-thunderbolt.x86_64              6.4.3-1.fc41   updates
plasma-vault.x86_64                    6.4.3-1.fc41   updates
plasma-welcome.x86_64                  6.4.3-1.fc41   updates
plasma-workspace.x86_64                6.4.3-1.fc41   updates
plasma-workspace-common.x86_64         6.4.3-1.fc41   updates
plasma-workspace-libs.x86_64           6.4.3-1.fc41   updates
plasma-workspace-wallpapers.noarch     6.4.3-1.fc41   updates
plasma5support.x86_64                  6.4.3-1.fc41   updates
polkit-kde.x86_64                      6.4.3-1.fc41   updates
powerdevil.x86_64                      6.4.3-1.fc41   updates
python3-boto3.noarch                   1.39.9-1.fc41  updates
python3-botocore.noarch                1.39.9-1.fc41  updates
python3-langtable.noarch               0.0.69-1.fc41  updates
qqc2-breeze-style.x86_64               6.4.3-1.fc41   updates
sddm-breeze.noarch                     6.4.3-1.fc41   updates
sddm-kcm.x86_64                        6.4.3-1.fc41   updates
sddm-wayland-plasma.noarch             6.4.3-1.fc41   updates
spectacle.x86_64                       1:6.4.3-1.fc41 updates
xdg-desktop-portal-kde.x86_64          6.4.3-1.fc41   updates

kaiman@kaiman:~$ find /sys -name "pwm*" 2>/dev/null
/sys/kernel/tracing/events/pwm
/sys/kernel/tracing/events/pwm/pwm_get
/sys/kernel/tracing/events/pwm/pwm_apply
/sys/kernel/tracing/events/pwm/pwm_write_waveform
/sys/kernel/tracing/events/pwm/pwm_read_waveform
/sys/kernel/tracing/events/pwm/pwm_round_waveform_fromhw
/sys/kernel/tracing/events/pwm/pwm_round_waveform_tohw
/sys/class/pwm
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_enable
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_min
/sys/devices/pci0000:00/0000:00:01.1/0000:10:00.0/0000:11:00.0/0000:12:00.0/hwmon/hwmon0/pwm1_max

(pelo visto não há, porque não imprimiu nada)
kaiman@kaiman:~$ modinfo amdgpu | grep -i navi33
kaiman@kaiman:~$

----------------------------------


