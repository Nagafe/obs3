# 🏥 SUHS - Sistema Unificado de Histórico de Saúde

> **Disciplina:** Arquitetura Orientada a Serviços (SOA)  
> **Alunos:** Nagafe de Oliveira Martins, Marcos Vinicius Siqueira Alves
> **Data:** 28 de Janeiro de 2026

---

## 1. O Problema
No cenário atual, os dados de saúde estão fragmentados.
* Um paciente atendido na **Rede Privada** não tem seu histórico acessível quando chega em uma **UBS (SUS)**.
* **Riscos:** Interações medicamentosas perigosas, repetição de exames caros e falta de informação em emergências.

## 2. A Solução: Arquitetura SOA
Propomos o **SUHS**, uma plataforma baseada em **Serviços Distribuídos**.
Não criamos um "banco de dados gigante", mas sim uma federação de serviços autônomos.

### 2.1. Os Serviços (Bounded Contexts)
Dividimos o domínio em 5 serviços independentes:
1.  **Identity Service:** Identificação única (UUID) do paciente.
2.  **Allergy Service:** Gestão de riscos e alergias.
3.  **Medication Service:** Histórico de prescrições.
4.  **Immunization Service:** Carteira de vacinação unificada.
5.  **Lab Service:** Resultados de exames.

---

## 3. Arquitetura Técnica
Adotamos o padrão **MVC (Model-View-Controller)** no Front-end consumindo serviços via **REST API**.

### Diagrama de Componentes
> *A aplicação Web atua como orquestradora, buscando dados em paralelo.*

![Diagrama de Componentes](diagrama1.png)


---

## 4. Estratégia de Integração
Para garantir performance e desacoplamento:

* **Identificadores:** Uso de **UUID** (ex: `a0eebc99...`) para unicidade global.
* **Comunicação:** JSON sobre HTTPS.
* **Resiliência:** Implementação de *Timeouts* e *Degradação Graciosa* (se o serviço de vacina cair, o resto do sistema continua funcionando).

### Fluxo de Dados (Diagrama de Sequência)
> *O Médico busca pelo CPF -> O sistema resolve o UUID -> Busca dados clínicos em paralelo.*

![Diagrama de Sequência](diagrama2.png)

---

## 5. Demonstração Prática (MVP)
Implementamos uma prova de conceito (PoC) da Camada de Controladores.
A demonstração abaixo simula a **latência de rede** e a **montagem assíncrona** do prontuário, provando que os dados vêm de fontes diferentes.

### 🚀 [CLIQUE AQUI PARA ACESSAR O SISTEMA AO VIVO](https://nagafe.github.io/obs3/)

---
*Projeto desenvolvido para a disciplina de Tecnologia de Sistemas para Internet - IFMT.*
