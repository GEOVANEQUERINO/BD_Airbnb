# Organização do Banco de Dados para o novo Airbnb

## Estrutura de Tabelas

### 1. Tabela: `usuarios`
- **Descrição:** Armazena informações dos usuários que utilizam o sistema (anfitriões ou hóspedes).  
- **Colunas:**
  - `id_usuario` (PK): Identificador único do usuário.
  - `nome`: Nome completo do usuário.
  - `email`: Endereço de email único.
  - `senha`: Senha para autenticação.
  - `telefone`: Número de contato.
  - `data_criacao`: Data de criação do cadastro.
- **Relacionamento:** Relaciona-se com a tabela `lugares` (1:N) e `hospedagens` (1:N).

---

### 2. Tabela: `lugares`
- **Descrição:** Representa os locais de hospedagem cadastrados pelos usuários anfitriões.
- **Colunas:**
  - `id_lugar` (PK): Identificador único do lugar.
  - `id_usuario` (FK): Referência ao usuário que cadastrou o lugar.
  - `nome`: Nome ou título do lugar.
  - `endereco`: Endereço completo do lugar.
  - `descricao`: Descrição detalhada da hospedagem.
  - `preco_diaria`: Valor da diária.
  - `data_cadastro`: Data de registro do lugar no sistema.
- **Relacionamento:** Relaciona-se com a tabela `hospedagens` (1:N).

---

### 3. Tabela: `hospedagens`
- **Descrição:** Registra os períodos em que os usuários fazem reservas em determinados lugares.
- **Colunas:**
  - `id_hospedagem` (PK): Identificador único da hospedagem.
  - `id_usuario` (FK): Referência ao usuário que fez a reserva.
  - `id_lugar` (FK): Referência ao lugar reservado.
  - `data_inicio`: Data de início da hospedagem.
  - `data_fim`: Data de término da hospedagem.
  - `valor_total`: Valor total da hospedagem (calculado com base no período e no preço da diária).
- **Relacionamento:** Relaciona-se com as tabelas `usuarios` e `lugares` (ambas 1:N).

---

### 4. Tabela: `avaliacoes`
- **Descrição:** Contém as avaliações feitas pelos usuários sobre hospedagens.
- **Colunas:**
  - `id_avaliacao` (PK): Identificador único da avaliação.
  - `id_hospedagem` (FK): Referência à hospedagem avaliada.
  - `id_usuario` (FK): Referência ao usuário que realizou a avaliação.
  - `nota`: Nota dada à hospedagem (ex.: de 1 a 5).
  - `comentario`: Comentário opcional do usuário.
  - `data_avaliacao`: Data em que a avaliação foi registrada.
- **Relacionamento:** Relaciona-se com as tabelas `usuarios` e `hospedagens` (ambas 1:N).

---

## Relacionamentos das Tabelas

1. **`usuarios` ↔ `lugares`:**
   - Relacionamento **1:N**.
   - Um usuário (anfitrião) pode cadastrar vários lugares.
   - FK em `lugares`: `id_usuario`.

2. **`usuarios` ↔ `hospedagens`:**
   - Relacionamento **1:N**.
   - Um usuário pode realizar várias hospedagens.
   - FK em `hospedagens`: `id_usuario`.

3. **`lugares` ↔ `hospedagens`:**
   - Relacionamento **1:N**.
   - Um lugar pode ser reservado por vários usuários em diferentes períodos.
   - FK em `hospedagens`: `id_lugar`.

4. **`hospedagens` ↔ `avaliacoes`:**
   - Relacionamento **1:1**.
   - Cada hospedagem pode receber apenas uma avaliação.
   - FK em `avaliacoes`: `id_hospedagem`.

5. **`usuarios` ↔ `avaliacoes`:**
   - Relacionamento **1:N**.
   - Um usuário pode fazer avaliações de várias hospedagens.
   - FK em `avaliacoes`: `id_usuario`.

---

## Justificativa das Decisões

1. **Separação por Entidades:** As tabelas foram criadas com base nas entidades principais do sistema (usuários, lugares, hospedagens e avaliações) para garantir modularidade e organização.

2. **Normalização:** O design evita redundância de dados, seguindo os princípios da normalização para garantir consistência e facilitar a manutenção.

3. **Facilidade de Consultas e Expansão:** Com a estrutura proposta, é possível implementar funcionalidades como busca de lugares, histórico de hospedagens, avaliações por lugar ou usuário, e relatórios de faturamento.

4. **Escalabilidade:** O modelo permite a expansão para novas funcionalidades, como métodos de pagamento, filtros de busca, e recursos adicionais nos lugares (ex.: fotos, comodidades).


