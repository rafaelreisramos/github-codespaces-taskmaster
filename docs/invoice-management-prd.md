# PRD - Sistema de Gerenciamento de Invoices

## 1. Visão Geral

### 1.1 Objetivo

Implementar um sistema completo de gerenciamento de invoices que permita o cadastro de empresas clientes, criação de invoices com múltiplos itens e geração de documentos PDF para download.

### 1.2 Contexto Técnico

- **Frontend**: Next.js (já implementado)
- **Backend**: Supabase (já implementado)
- **Autenticação**: Implementada
- **Perfil de usuário**: Implementado

### 1.3 Escopo

- Gerenciamento de dados da empresa emissora
- Cadastro e gerenciamento de empresas clientes
- Criação e edição de invoices
- Gerenciamento de itens por invoice
- Geração de PDF para download

## 2. Requisitos Funcionais

### 2.1 Gerenciamento da Empresa Emissora

#### RF001 - Cadastro de Dados da Empresa

**Descrição**: O sistema deve permitir que a empresa mantenha seus dados atualizados.

**Critérios de Aceitação**:

- [ ] Formulário para inserção/edição dos dados da empresa
- [ ] Campos obrigatórios: Razão Social, CNPJ, Endereço, Pessoa de Contato, Email
- [ ] Validação de CNPJ
- [ ] Validação de email
- [ ] Apenas um registro de empresa por usuário/organização
- [ ] Dados salvos automaticamente ou com confirmação explícita

**Dados da Empresa**:

- Razão Social (obrigatório)
- CNPJ (obrigatório, com validação)
- Endereço Completo (obrigatório)
  - Logradouro
  - Número
  - Complemento (opcional)
  - Bairro
  - Cidade
  - Estado
  - CEP
- Pessoa de Contato (obrigatório)
- Email de Contato (obrigatório)
- Telefone (opcional)
- Logo da Empresa (opcional)

### 2.2 Gerenciamento de Empresas Clientes

#### RF002 - Cadastro de Clientes

**Descrição**: O sistema deve permitir cadastrar e gerenciar empresas clientes.

**Critérios de Aceitação**:

- [ ] Lista de clientes cadastrados
- [ ] Formulário de cadastro de novo cliente
- [ ] Formulário de edição de cliente existente
- [ ] Busca e filtros na lista de clientes
- [ ] Exclusão de clientes (com confirmação)
- [ ] Validação de campos obrigatórios

**Dados do Cliente**:

- Razão Social (obrigatório)
- CNPJ/CPF (obrigatório, com validação)
- Endereço Completo (obrigatório)
- Pessoa de Contato (obrigatório)
- Email (obrigatório)
- Telefone (opcional)
- Observações (opcional)

#### RF003 - Listagem e Busca de Clientes

**Descrição**: Interface para visualizar e buscar clientes cadastrados.

**Critérios de Aceitação**:

- [ ] Tabela responsiva com lista de clientes
- [ ] Busca por nome/razão social
- [ ] Filtro por CNPJ/CPF
- [ ] Paginação quando necessário
- [ ] Ações: Editar, Excluir, Ver Invoices

### 2.3 Gerenciamento de Invoices

#### RF004 - Criação de Invoice

**Descrição**: O sistema deve permitir criar novas invoices para clientes cadastrados.

**Critérios de Aceitação**:

- [ ] Seleção de cliente da lista
- [ ] Preenchimento de dados da invoice
- [ ] Adição de múltiplos itens
- [ ] Cálculo automático de totais
- [ ] Validação de campos obrigatórios
- [ ] Salvamento como rascunho ou finalização

**Dados da Invoice**:

- Número da Invoice (gerado automaticamente)
- Cliente (seleção obrigatória)
- Data de Emissão (padrão: data atual)
- Data de Vencimento (obrigatório)
- Descrição/Observações (opcional)
- Status (Rascunho, Enviada, Paga, Vencida)
- Valor Total (calculado automaticamente)

#### RF005 - Gerenciamento de Itens da Invoice

**Descrição**: Cada invoice deve permitir adicionar, editar e remover itens.

**Critérios de Aceitação**:

- [ ] Adicionar novo item à invoice
- [ ] Editar item existente
- [ ] Remover item da invoice
- [ ] Cálculo automático do total por item
- [ ] Cálculo automático do total geral
- [ ] Validação de valores numéricos

**Dados do Item**:

- Descrição (obrigatório)
- Quantidade (obrigatório, numérico)
- Valor Unitário (obrigatório, numérico)
- Total do Item (calculado: quantidade × valor unitário)

#### RF006 - Listagem de Invoices

**Descrição**: Interface para visualizar todas as invoices criadas.

**Critérios de Aceitação**:

- [ ] Tabela com lista de invoices
- [ ] Informações: Número, Cliente, Data, Valor, Status
- [ ] Busca por número da invoice
- [ ] Filtro por cliente
- [ ] Filtro por status
- [ ] Filtro por período (data)
- [ ] Ordenação por colunas
- [ ] Ações: Editar, Visualizar, Download PDF, Excluir

#### RF007 - Edição de Invoice

**Descrição**: Permitir editar invoices existentes.

**Critérios de Aceitação**:

- [ ] Edição apenas de invoices em rascunho ou enviadas
- [ ] Preservar histórico de alterações
- [ ] Atualização automática de totais
- [ ] Validação de dados

### 2.4 Geração de PDF

#### RF008 - Download de Invoice em PDF

**Descrição**: Gerar documento PDF formatado com os dados da invoice.

**Critérios de Aceitação**:

- [ ] Layout profissional e responsivo
- [ ] Dados da empresa emissora no cabeçalho
- [ ] Dados do cliente
- [ ] Tabela de itens com totais
- [ ] Total geral destacado
- [ ] Numeração sequencial
- [ ] Download imediato do arquivo
- [ ] Nome do arquivo: "Invoice*[NUMERO]*[CLIENTE].pdf"

**Conteúdo do PDF**:

- Logo da empresa (se cadastrado)
- Dados completos da empresa emissora
- Dados completos do cliente
- Número da invoice e datas
- Tabela detalhada de itens
- Subtotais e total geral
- Observações (se houver)

## 3. Requisitos Não Funcionais

### 3.1 Performance

- RF009: O sistema deve responder em até 2 segundos para operações básicas
- RF010: Geração de PDF deve ser concluída em até 5 segundos
- RF011: Lista de invoices deve carregar com paginação para mais de 50 registros

### 3.2 Usabilidade

- RF012: Interface responsiva para desktop e mobile
- RF013: Validação em tempo real nos formulários
- RF014: Mensagens de feedback claras para todas as ações
- RF015: Navegação intuitiva entre as seções

### 3.3 Segurança

- RF016: Todas as operações devem respeitar o contexto do usuário logado
- RF017: Validação de dados no frontend e backend
- RF018: Sanitização de inputs para prevenir XSS

### 3.4 Compatibilidade

- RF019: Suporte aos navegadores Chrome, Firefox, Safari e Edge (últimas 2 versões)
- RF020: PDFs compatíveis com visualizadores padrão

## 4. Modelo de Dados

### 4.1 Tabela: companies

```sql
- id (uuid, primary key)
- user_id (uuid, foreign key para auth.users)
- razao_social (text, not null)
- cnpj (text, not null, unique)
- endereco_logradouro (text, not null)
- endereco_numero (text, not null)
- endereco_complemento (text)
- endereco_bairro (text, not null)
- endereco_cidade (text, not null)
- endereco_estado (text, not null)
- endereco_cep (text, not null)
- pessoa_contato (text, not null)
- email_contato (text, not null)
- telefone (text)
- logo_url (text)
- created_at (timestamp)
- updated_at (timestamp)
```

### 4.2 Tabela: clients

```sql
- id (uuid, primary key)
- company_id (uuid, foreign key para companies)
- razao_social (text, not null)
- cnpj_cpf (text, not null)
- endereco_logradouro (text, not null)
- endereco_numero (text, not null)
- endereco_complemento (text)
- endereco_bairro (text, not null)
- endereco_cidade (text, not null)
- endereco_estado (text, not null)
- endereco_cep (text, not null)
- pessoa_contato (text, not null)
- email (text, not null)
- telefone (text)
- observacoes (text)
- created_at (timestamp)
- updated_at (timestamp)
```

### 4.3 Tabela: invoices

```sql
- id (uuid, primary key)
- company_id (uuid, foreign key para companies)
- client_id (uuid, foreign key para clients)
- numero (text, not null, unique per company)
- data_emissao (date, not null)
- data_vencimento (date, not null)
- descricao (text)
- status (enum: 'rascunho', 'enviada', 'paga', 'vencida')
- valor_total (decimal, calculated)
- created_at (timestamp)
- updated_at (timestamp)
```

### 4.4 Tabela: invoice_items

```sql
- id (uuid, primary key)
- invoice_id (uuid, foreign key para invoices)
- descricao (text, not null)
- quantidade (decimal, not null)
- valor_unitario (decimal, not null)
- valor_total (decimal, calculated)
- ordem (integer, not null)
- created_at (timestamp)
- updated_at (timestamp)
```

## 5. Fluxos de Usuário

### 5.1 Fluxo Principal: Criar Invoice

1. Usuário acessa seção de Invoices
2. Clica em "Nova Invoice"
3. Seleciona cliente (ou cadastra novo)
4. Preenche dados básicos da invoice
5. Adiciona itens um por um
6. Revisa totais calculados
7. Salva como rascunho ou finaliza
8. Faz download do PDF

### 5.2 Fluxo Secundário: Cadastrar Cliente

1. Acessa seção de Clientes
2. Clica em "Novo Cliente"
3. Preenche formulário
4. Valida dados
5. Salva cliente

### 5.3 Fluxo de Configuração: Dados da Empresa

1. Acessa configurações/perfil
2. Seção "Dados da Empresa"
3. Preenche/edita informações
4. Salva alterações

## 6. Interfaces de Usuário

### 6.1 Layout Principal

- Sidebar com navegação: Dashboard, Invoices, Clientes, Configurações
- Header com informações do usuário
- Área principal responsiva

### 6.2 Telas Principais

1. **Dashboard**: Resumo de invoices recentes, valores, estatísticas
2. **Lista de Invoices**: Tabela com filtros e busca
3. **Criar/Editar Invoice**: Formulário com seção de itens
4. **Lista de Clientes**: Tabela com ações
5. **Cadastro de Cliente**: Formulário responsivo
6. **Configurações da Empresa**: Formulário de dados

## 7. Critérios de Aceitação Técnicos

### 7.1 Frontend (Next.js)

- Componentes reutilizáveis para formulários
- Gerenciamento de estado (Context API ou Zustand)
- Validação com React Hook Form + Zod
- UI Library (shadcn/ui ou similar)
- Responsividade com Tailwind CSS

### 7.2 Backend (Supabase)

- RLS (Row Level Security) configurado
- Functions para cálculos complexos
- Triggers para campos calculados
- Policies de acesso por usuário

### 7.3 Geração de PDF

- Biblioteca: jsPDF + html2canvas ou Puppeteer
- Template HTML/CSS para layout
- Compressão otimizada
- Fallback para erros

## 8. Fases de Implementação

### Fase 1: Estrutura Base

- [ ] Modelo de dados no Supabase
- [ ] Configuração RLS
- [ ] Telas básicas de navegação

### Fase 2: Gerenciamento de Dados

- [ ] CRUD de empresa
- [ ] CRUD de clientes
- [ ] Validações e formulários

### Fase 3: Sistema de Invoices

- [ ] CRUD de invoices
- [ ] Gerenciamento de itens
- [ ] Cálculos automáticos

### Fase 4: Geração de PDF

- [ ] Template de PDF
- [ ] Integração de download
- [ ] Testes e otimizações

### Fase 5: Polimentos

- [ ] Dashboard com métricas
- [ ] Melhorias de UX
- [ ] Testes finais

## 9. Considerações Técnicas

### 9.1 Numeração de Invoices

- Sequencial por empresa
- Formato: INV-YYYY-NNNN
- Implementar via Supabase Function

### 9.2 Cálculos

- Campos calculados via triggers
- Validação no frontend e backend
- Precisão decimal adequada

### 9.3 Upload de Logo

- Integração com Supabase Storage
- Validação de formato e tamanho
- Redimensionamento automático

### 9.4 Backup e Auditoria

- Log de alterações importantes
- Soft delete para registros críticos
- Backup automático do Supabase

## 10. Testes

### 10.1 Testes Unitários

- Funções de cálculo
- Validações de formulário
- Componentes React

### 10.2 Testes de Integração

- Fluxos completos de CRUD
- Geração de PDF
- Autenticação e autorização

### 10.3 Testes de Usabilidade

- Navegação intuitiva
- Responsividade
- Performance em dispositivos diversos

---

**Observações Finais**:
Este PRD serve como guia para implementação. Detalhes específicos podem ser refinados durante o desenvolvimento conforme necessidades técnicas e feedback de usuários.
