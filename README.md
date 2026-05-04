# Riemenn-Engine

Engine (Motor gráfico) & Jogo/App de simulação espacial.

**Sobre o projeto sinistrasso:**

Simulação do sistema solar real, iniciando no periodo padrão (Nasa J2000) e mudando a data para a atual, por exemplo, o simulador calculará a posicão exata dos planetas do dia atual. 
Niveis técnicos e didáticos que nao afetam funcionamento: Tamanhos e distancias reais **OU** Tamanhos e distancias humanamente compreensiveis, para entendimento didático real e factual sem dificuldades.
Dados e estatisticas reais! O simulador nao sabe que um ano terrestre dura 365 dias, ou o que é um ano bissexto, ele calcula em tempo real o fim da translação da terra e nos da o resultados em dias humanos; o principal foco do simulador é esse! ELe nao trabalha com quase nenhuma instrução, ele calcula! Outro exemplo é que ele não sabe que a terra custuma de aproximar do sól em certos periodos, mas ele calcula em tempo real e devolve o resultado na sua tela, completamente compativel com a realidade!

Isso se deve aos calculos como os de Riemenn, Einsten (relatividade e espaço/tempo) e alguns de Hawking. São os mesmos calculos que nos possibilitam saber de informaçoes interestelares, é como uma visualização real das contas de lousa. 
Existem outros softwares didaticos da Nasa e SpaceX que fazem a mesma coisa, com foco didático, mas não focados em engenharia de software.


**Técnico (Parte chata, ou a parte mais legal dependendo da sua area):**

Baseado em C puro (por hobby, ou loucura, fica a seu critério), com HAL (Abstração de Hardware) e PAL (Abstração de Plataforma).
Usa Backends para Vulkan, OpenGL, Direct3D e Metal; sendo Metal e Vulkan os mais estáveis. Estas são bibliotecas de baixo nivel para placa de video/GPU que permitem renderização gráfica em plataformas.
Possui PAL para renderização em Windows (Via Win32, essa API tenebrosa), Apple (via Cocoa e WebKit) e para sistemas como linux usando os ambientes Wayland e X11.
A arquitetura do software é focada em otimização enorme para melhor aplicação no hardware do usuário, como por exemplo: Usar GPU para calcular gravidade e fisica se disponivel **OU** Usar outros núcleos da CPU para isso, fazendo uma simulação perfeita pro usuário.
Bibliotecas nativas: Basicamente nenhuma biblioteca adicional/externa (se considerarmos as APIs de renderização e Plataforma como obrigatórias)
Roda em navegadores via WebAssembly e WebGPU!



## Setup 
**Compile com cmake (recomendado) ou rode o wrapper Make (Menos configuravel.)**


```bash
# 1. Configurar (Auto-Detect)
cmake -S . -B build

# 2. Compilar
cmake --build build --parallel $(nproc)
```

### Overrides Manuais

exemplo: Forçar Wayland + Vulkan:
```bash
cmake -S . -B build -DPLATFORM=LINUX_WAYLAND -DGPU_API=vulkan
```

Exemplo: Forçar Windows + DX11:
```bash
cmake -S . -B build -DPLATFORM=WINDOWS -DGPU_API=dx11
```


CMake detecta automaticamente a plataforma e a API grafica recomendada, se você quiser usar outra API, rode o cmake (ou wrapper make) com a flag especifica (Tipo, quando optar usar opengl ao invés do padrão vulkan. )


# Plataformas e APIs graficas:

  linux-x11       **(Default: vulkan | Opções: opengl**)

  linux-wayland   **(Default: vulkan | Opções: opengl**)

  fbsd-x11        **(Default: vulkan | Opções: opengl**)

  fbsd-wayland    **(Default: vulkan | Opções: opengl**)

  windows         **(Default: dx11   | Opções: vulkan, opengl**)

  mac             **(Default: metal  | Apenas Apple Silicon**)

  mac_x86         **(Default: metal  | Intel - Suporta, porém deprecated: opengl**)

  navigator       **(Default: webgpu | Nenhuma outra opção**)




Recomendado usar clang-llvm ou apple-clang (o melhor em apple). Não foi testado em outros compiladores e pode dar problemas com flags!


