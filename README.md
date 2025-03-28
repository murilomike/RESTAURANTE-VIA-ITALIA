# Projeto: Implantação da Instância do Restaurante VIA ITALIA

Este repositório contém toda a documentação e passos realizados durante o projeto acadêmico **"Restaurante VIA ITALIA"**, desenvolvido para aprender o ciclo completo das atividades de um DBA em um ambiente SQL Server. Lembre-se: o ambiente é acadêmico, mas as práticas aplicadas refletem boas práticas do mercado!

---

## Índice

- [Objetivo Geral](#objetivo-geral)
- [Análise de Requisitos](#análise-de-requisitos)
- [Definição do Projeto](#definição-do-projeto)
- [Implementação e Configuração](#implementação-e-configuração)
  - [Hardware](#hardware)
  - [Software](#software)
  - [Instalação do SQL Server](#instalação-do-sql-server)
  - [Configuração da Instância e Diretórios](#configuração-da-instância-e-diretórios)
  - [Configuração de Rede e Firewall](#configuração-de-rede-e-firewall)
  - [Criação de Aliases e Logins](#criação-de-aliases-e-logins)
  - [Ajustes de Performance e Configuração Adicionais](#ajustes-de-performance-e-configuração-adicionais)
- [Testes e Validações](#testes-e-validações)
- [Conclusão](#conclusão)
- [FAQ](#faq)

---

## Objetivo Geral

O projeto teve como objetivo aprender o ciclo completo de atividades de um DBA, passando pelas seguintes fases:
- **Análise de Requisitos**
- **Definição do Projeto**
- **Implementação**
- **Testes**
- **Acompanhamento**

---

## Análise de Requisitos

Para o Restaurante VIA ITALIA, os requisitos foram:

- **Usuários Simultâneos:**  
  Inicialmente 15 usuários, escalonando para 40.
- **Infraestrutura:**  
  - Sem servidor pré-existente – necessidade de recomendação.
  - Uso de collation: `Latin General CI AI`.
  - Licenciamento: SQL Server Standard (licenciamento por núcleo; uso de trial inicialmente).
- **Hardware Recomendado:**  
  - Disco: SSD (priorizando performance mesmo com menor espaço).  
  - Memória:  
    - Primeiro ano: 4 GB (aproximadamente 3 GB para uso do SQL Server).  
    - Após 6 meses: Upgrade para 6,5 GB podendo chegar a 9,5 GB, dependendo do cenário.
  - Processador: Intel Xeon com 4 núcleos.
  - Possibilidade de expansão para servidores com maior capacidade (cerca de 12 GB de memória, por exemplo).

---

## Definição do Projeto

**Cronograma e Responsabilidades:**
- Entender as responsabilidades do DBA versus as da equipe de infraestrutura.
- Prever o tempo de 1 a 2 dias para a configuração inicial do ambiente.
- Planejar os períodos de homologação e entrega da instância.

---

## Implementação e Configuração

### Hardware

- **Disco:** SSD.
- **Memória:** Configuração inicial de 8 GB (além de reserva de 4 GB).
- **Processador:** Intel Xeon (4 núcleos).

### Software

- **Sistema Operacional:** Windows Server 2016.
- **SQL Server:** Utilizei a versão 2016 em edição Trial (com Service Pack 3 e Cumulative Update).
- **Serviços Importantes:**  
  - Integration Services
  - SQL Server Agent

### Instalação do SQL Server

1. Baixei a versão do SQL Server 2016 juntamente com as atualizações (Service Pack 3 e Cumulative Update).
2. Durante a instalação, optei por uma instância nomeada, conforme a orientação do projeto.
3. Verifiquei a necessidade de instalar apenas os componentes essenciais (Integration Services e SQL Agent).

### Configuração da Instância e Diretórios

- **Separação de Pastas:**  
  - Criação de um diretório exclusivo para os arquivos de dados.
  - Criação de um diretório exclusivo para os arquivos de log.
- **Arquivo de Backup:**  
  - Definição de um diretório dedicado para armazenar os backups.
- **TEMPDB:**  
  - Criação de arquivos de dados e log conforme o número de núcleos do servidor (por exemplo, 1 arquivo por núcleo).
  - Configuração do tamanho inicial e dos valores de auto crescimento (ex.: 1.024 MB iniciais com crescimento de 512 MB para os dados do TEMPDB).

### Configuração de Rede e Firewall

- **Porta Padrão:**  
  - A instância padrão do SQL Server usa a porta 1433.
  - Para este projeto, alterei a porta para um valor customizado (por exemplo, 15987).
- **Firewall:**  
  - Habilitei os perfis (domínio, particular e público).
  - Criei a regra de entrada para permitir conexões TCP pela porta customizada.

### Criação de Aliases e Logins

- **Aliases:**  
  - Criei um alias com a designação “SQLVIAITALIA” para facilitar futuras migrações sem precisar alterar a connection string.
- **Logins:**  
  - Inicialmente, utilizei o logon SA e o logon via Windows (modo misto).
  - Após o primeiro login, desabilitei o logon SA e criei um novo login administrativo (manutAdmin) com autenticação SQL.
  - Em paralelo, criei um usuário específico para acesso à base de dados (userSISTEMA), isolando a administração da instância do acesso à aplicação.

### Ajustes de Performance e Configuração Adicionais

- **Memória da Instância:**  
  - Ajustei a “max server memory” para cerca de 4906 MB.
- **Configuração de Auto-Growth:**  
  - Para os arquivos de dados e logs, configurei tamanhos iniciais e incrementos automáticos baseados em porcentagens do espaço (por exemplo, 10% de 1 GB ou 1% para bases maiores).
- **Outros Ajustes:**  
  - Configurei opções como “Estatística Automática” e “Auto Close” conforme as necessidades do ambiente.

---

## Testes e Validações

Após concluir a instalação e as configurações, realizei os seguintes testes:
- Testei o acesso via alias utilizando o SSMS.
- Verifiquei os logs e monitorizei os serviços do SQL Server.
- Realizei backups simples para validar as configurações dos diretórios.

---

## Conclusão

O projeto "Restaurante VIA ITALIA" foi concluído com êxito, permitindo-me colocar em prática diversos conhecimentos fundamentais do ciclo de atividades do DBA – desde a análise de requisitos e planejamento, até a instalação, configuração e ajustes do ambiente SQL Server. Esse repositório serve como documentação e referência para futuros projetos e estudos na área.

---

## FAQ

**1. Qual versão do SQL Server foi utilizada?**  
Utilizei a versão 2016 em edição Trial, atualizada com Service Pack 3 e o Cumulative Update.

**2. Por que optei por uma instância nomeada?**  
Uma instância nomeada facilita a organização e a identificação do ambiente, além de permitir a configuração de portas e aliases personalizados para futuras migrações.

**3. Como foi configurado o TEMPDB?**  
Adaptei a quantidade de arquivos do TEMPDB para corresponder ao número de núcleos do servidor, e configurei tanto o tamanho inicial quanto o auto-growth para otimizar a performance.

**4. O que foi configurado no Firewall?**  
Alterei a porta padrão do SQL Server para uma porta customizada (por exemplo, 15987) e configurei as regras de entrada para habilitar conexões TCP em todos os perfis (domínio, particular e público).

**5. Quais práticas de segurança foram adotadas?**  
Desabilitei o logon SA e criei um login administrativo exclusivo (manutAdmin). Também separei o usuário de administração do usuário de acesso à aplicação, promovendo maior segurança e isolamento.

