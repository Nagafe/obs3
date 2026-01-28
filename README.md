# 🏥 SUHS - Sistema Unificado de Histórico de Saúde

> **Disciplina:** Arquitetura Orientada a Serviços (SOA)  
> **Alunos:** Nagafe de Oliveira Martins, Marcos Vinicius Siqueira Alves
> **Data:** 28 de Janeiro de 2026

---

## 1. O Desafio: Ecossistema de Saúde Desintegrado
O maior obstáculo da saúde no Brasil não é a falta de dados, mas a falta de conexão entre as diferentes esferas de atendimento. Hoje, a jornada do paciente é interrompida cada vez que ele muda de instituição.

O nosso desafio é **emplacar a integração total**, unificando quatro universos que hoje operam isolados:

1.  🏥 **Esfera Municipal:** Unidades Básicas (UBS) e UPAs (Porta de entrada).
2.  🏥 **Esfera Estadual:** Hospitais Regionais e Centros de Referência (Alta complexidade).
3.  🏥 **Esfera Federal:** Hospitais Universitários e Institutos de Pesquisa.
4.  🏥 **Esfera Privada:** Clínicas, Laboratórios e Hospitais Particulares.

**O Problema:** Sem uma arquitetura que suporte essa diversidade, o paciente "reinicia" seu histórico a cada atendimento, gerando riscos clínicos e desperdício de recursos.
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

![Diagrama de Componentes](https://github.com/Nagafe/obs3/blob/main/Diagrama1.png)


---

## 4. Estratégia de Integração
Para garantir performance e desacoplamento:

* **Identificadores:** Uso de **UUID** (ex: `a0eebc99...`) para unicidade global.
* **Comunicação:** JSON sobre HTTPS.
* **Resiliência:** Implementação de *Timeouts* e *Degradação Graciosa* (se o serviço de vacina cair, o resto do sistema continua funcionando).

### Fluxo de Dados (Diagrama de Sequência)
> *O Médico busca pelo CPF -> O sistema resolve o UUID -> Busca dados clínicos em paralelo.*

![Diagrama de Sequência](https://github.com/Nagafe/obs3/blob/main/Diagrama2.png)

---

## 5. Demonstração Prática (MVP)
Implementamos uma prova de conceito (PoC) da Camada de Controladores.
A demonstração abaixo simula a **latência de rede** e a **montagem assíncrona** do prontuário, provando que os dados vêm de fontes diferentes.


---
## 6. Conclusão e Resultados
O projeto SUHS valida a aplicação da **Arquitetura Orientada a Serviços (SOA)** como a solução viável para o problema histórico da interoperabilidade na saúde brasileira.

A prova de conceito demonstrou que:

1.  **Integração Viável:** É possível conectar sistemas heterogêneos das quatro esferas (**Municipal, Estadual, Federal e Privada**) sem exigir que elas substituam seus softwares legados, utilizando **REST APIs** como camada de tradução universal.
2.  **Segurança e Autonomia:** O uso de **UUIDs** e bancos de dados isolados respeita a governança de cada instituição, garantindo que o prontuário seja único mesmo vindo de fontes diferentes.
3.  **Resiliência:** A arquitetura descentralizada provou ser robusta; falhas em serviços periféricos (ex: Vacinas) não derrubam o atendimento de emergência, garantindo a continuidade do cuidado.

**Em resumo:** O SUHS transforma a fragmentação de dados em um ecossistema colaborativo, onde a tecnologia atua diretamente na prevenção de erros médicos e na otimização de recursos públicos e privados.

### 🚀 [CLIQUE AQUI PARA ACESSAR O SISTEMA AO VIVO](https://nagafe.github.io/obs3/)

---
*Projeto desenvolvido para a disciplina de Tecnologia de Sistemas para Internet - IFMT.*
