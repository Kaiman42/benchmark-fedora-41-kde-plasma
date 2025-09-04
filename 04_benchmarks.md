# Resultados de Benchmarks

## Teste de Desempenho com glxgears
```
300 frames in 5.0 seconds = 60.000 FPS
300 frames in 5.0 seconds = 59.987 FPS
300 frames in 5.0 seconds = 60.000 FPS
```
- **GPU em uso**: AMD Radeon RX 7600 (única ativa)
- **Resolução**: 2560x1080
- **VSync**: Ativado (limite de 60 FPS)

## Teste com glmark2
```
=======================================================
    glmark2 2023.01
=======================================================
    OpenGL Information
    GL_VENDOR:      AMD
    GL_RENDERER:    AMD Radeon RX 7600 (radeonsi, navi33, LLVM 20.1.8, DRM 3.64, 6.16.3-200.fc42.x86_64)
    GL_VERSION:     4.6 (Compatibility Profile) Mesa 25.1.7
    Surface Config: buf=32 r=8 g=8 a=8 depth=24 stencil=0 samples=0
    Surface Size:   800x600 windowed
=======================================================
[build] use-vbo=false: FPS: 9914 FrameTime: 0.101 ms
=======================================================
                                  glmark2 Score: 9913 
```
- **GPU em uso**: AMD Radeon RX 7600 (única ativa)
- **Score**: 9913 (alta performance confirmada)

## Monitoramento com nvtop
- **Uso de GPU**: <10% em repouso, <100% sob carga
- **Uso de VRAM**: ~271MiB em repouso, até 7.984GiB disponível
- **Clock da Memória**: 1.124 GHz (varia com carga)
- **Clock do Shader**: 0.5 GHz em repouso, até 1.9 GHz
- **Temperatura**: 52°C em repouso, ventoinha ativa sob carga
- **FAN**: 0% em repouso, aumenta automaticamente

## Uso de Recursos
- **Uso de VRAM em repouso**: 271MiB de 7.984GiB
- **Clock da Memória**: 1.124 GHz (varia)
- **Clock do Shader**: 0.5 GHz (21% do máximo)
- **Temperatura em repouso**: 52°C
- **Ventoinha**: Gira automaticamente sob carga (12 RPM observado)

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
- **Overdrive**: Desabilitado (parâmetro amdgpu.ppfeaturemask=0x0)
- **VRAM Total**: 8.176GiB (RX 7600, única ativa)
- **Driver AMDGPU**: 3.63.0

### Controle de Ventoinhas
- **Status**: Automático (gira sob carga)
- **Arquivos de Controle**: Disponíveis em `/sys/devices/.../hwmon/hwmon0/pwm1*`
- **Temperatura em Repouso**: ~52°C

## Observações
- Sistema usa apenas GPU dedicada (iGPU desabilitada no BIOS).
- Métricas corretas com nvtop (sem uso >100%).
- Ventoinha funciona automaticamente.
- SMU inicializada com sucesso.
- Nenhum problema de timeout detectado após correções.

## Atualizações Disponíveis (Fedora 41)
- Várias atualizações do KDE Plasma 6.4.3 para 6.4.4 disponíveis.
- Nenhuma atualização crítica do kernel ou drivers AMD no momento.
