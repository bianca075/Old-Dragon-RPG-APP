# Old Dragon RPG — Android (Kotlin)

Aplicativo Android para criação e gestão de personagens de RPG, utilizado como prática estruturada de Android nativo, organização de domínio e persistência local.

## Objetivos do projeto
- Modelar o domínio de personagens (raças, classes e atributos).
- Implementar fluxo de telas em etapas para criação de personagem.
- Persistir dados localmente com Room e consulta reativa via Flow.
- Manter código organizado em camadas e pacotes coerentes.

## Stack técnica
- Linguagem: Kotlin
- UI: Activities com componentes em Jetpack Compose
- Persistência: Room (Entity, DAO, Database) + Flow
- Build: Gradle
- SDK alvo: compileSdk/targetSdk 36

## Estrutura do código (resumo)
rpgApp/
└─ app/src/main/java/com/example/myapplication/
├─ controller/ # MainActivity1..6 (etapas) + PersonagensDebugActivity
├─ data/
│ ├─ dao/ # PersonagemDao (operações CRUD + Flow)
│ ├─ db/ # AppDatabase (singleton: old_dragon2.db)
│ ├─ entity/ # PersonagemEntity
│ └─ repository/ # PersonagemRepository (orquestra o DAO)
├─ model/ # domínio: atributos, raças, classes, distribuição
└─ ui/theme/ # theming e estilos


## Domínio
- Atributos: Força, Destreza, Constituição, Inteligência, Sabedoria, Carisma.
- Raças e classes: estruturas base para composição do personagem.
- Métodos de distribuição de atributos: regras simples para diferentes perfis.

## Persistência (Room)
- `PersonagemEntity`: campos para nome, raça, classe e atributos.
- `PersonagemDao`:
  - `inserir`, `atualizar`, `deletar`
  - `listarTodos(): Flow<List<PersonagemEntity>>`
  - `buscarPorId(id): Flow<PersonagemEntity?>`
- `AppDatabase`: singleton que abre `old_dragon2.db`.
- `PersonagemRepository`: centraliza o acesso ao DAO e expõe operações para a camada de UI.

## Fluxo de telas
- `MainActivity1` → `MainActivity6`: etapas de criação do personagem (formulário em passos).
- `PersonagensDebugActivity`: listagem e inspeção de personagens salvos.
- UI com Jetpack Compose nas telas (ex.: resumo final), gerenciamento de estado local com `remember`/`mutableStateOf`.

## Como executar
1. Requisitos:
   - Android Studio (JDK 17)
   - Emulador API 24+ ou dispositivo físico
2. Abrir o projeto:
   - File > Open… e selecione a pasta do projeto (`rpgApp`)
   - Aguarde a sincronização do Gradle
3. Executar:
   - Selecione um dispositivo ou emulador
   - Clique em Run

## Boas práticas adotadas
- Separação em pacotes por responsabilidade (`controller`, `data`, `model`).
- Repositório intermediando acesso a dados.
- Consultas reativas com Flow para listagens.
- Telas em etapas para clareza de formulário e validação simples.

## Roadmap curto
- Unificar navegação em uma Activity com Navigation/Compose.
- Autosave de formulário com DataStore.
- Exportar/Importar personagem em JSON.
- Melhorias de acessibilidade e tema escuro.
