# Sprint1 Soluções Energéticas

ChargeGrid Intelligence: Mobilidade Elétrica e Eficiência Sustentável no Varejo

Este repositório contém a documentação da solução **ChargeGrid Intelligence**, desenvolvida para o EV Challenge FIAP + GoodWe 2026, com foco na integração entre mobilidade elétrica, gestão de dados e sustentabilidade arquitetônica no setor comercial.

---

## 👥 Equipe

| Nome | RM |
|------|----|
Gabriel Fagundes | RM: 569074
Gabriel Freitas | RM: 572943
Giovanni Merlotti | RM: 573721
Glauco Kelly | RM: 572840
Sergio Augusto Amaral | RM: 570184
Thiago Renatino | RM: 569073

---

## 🛑 Problema e Justificativa
A transição da mobilidade elétrica para o ambiente comercial (varejo, shoppings, supermercados) esbarra em um limite físico grave: a capacidade da rede elétrica local. 

A instalação de múltiplos eletropostos (como o modelo HCA G2 de 22 kW da GoodWe) sem orquestração de potência gera picos de consumo simultâneos. Isso resulta na ultrapassagem da demanda contratada junto à distribuidora, acarretando multas severas (sob a Resolução ANEEL nº 1.000/2021) e o risco de desarmamento de todo o circuito elétrico do estabelecimento. 

Atualmente, a ausência de mecanismos integrados para orquestrar essa potência, registrar ciclos e faturar a energia inviabiliza a adoção escalável e segura de carregadores no comércio.

---

## 💡 Proposta e Impactos Esperados
O **ChargeGrid Intelligence** resolve esse problema transformando carregadores isolados em um ecossistema inteligente. Em vez de atuar apenas como hardware de recarga, o sistema atua como um gerenciador de energia em malha fechada.

**Como funciona:**
Nossa arquitetura monitora a demanda elétrica da loja a cada 30 segundos via protocolo MODBUS. Caso o consumo do estabelecimento (ex: acionamento de ar-condicionado) chegue perto do limite crítico da rede, nossa API envia um comando (via protocolo OCPP) que reduz imediatamente a potência entregue aos veículos no estacionamento.

**Impactos Esperados:**
1. **Segurança Operacional:** Eliminação completa do risco de quedas de energia e multas por ultrapassagem de demanda.
2. **Viabilidade Econômica:** Precificação dinâmica da energia através do gateway Abacate Pay, transformando o carregador em uma nova linha de receita sustentável para o varejista.
3. **Escalabilidade:** Interoperabilidade garantida por protocolos abertos, impedindo o *lock-in* tecnológico.

---

## 🌍 A Ótica da Sustentabilidade e Eficiência Energética
A verdadeira sustentabilidade não se resume a colocar veículos limpos nas ruas, mas em **como otimizamos a rede de energia que já existe**.

Historicamente, para adicionar eletropostos em um comércio, o lojista precisaria realizar obras civis pesadas: quebrar asfalto, aumentar a espessura de cabos de cobre, usar cimento e desperdiçar materiais físicos para expandir a infraestrutura elétrica. 

O ChargeGrid Intelligence promove a **Sustentabilidade por Software**:
Através do conceito de *Abstração*, nós transferimos o limite elétrico do mundo físico para o nosso código Python. O Controle de Demanda Inteligente permite que o estabelecimento suporte veículos elétricos de alta potência aproveitando a ociosidade da rede atual, garantindo eficiência energética máxima sem o impacto ambiental, financeiro e logístico da quebra de infraestrutura.

---

## ⚙️ Tecnologias Utilizadas
A arquitetura foi desenhada para operar com altíssima disponibilidade e latência inferior a 5 segundos no controle de potência.

* **Backend / Lógica Central:** `Python` com framework `FastAPI`, responsável pela agilidade e integração de APIs analíticas em tempo real.
* **Inteligência Artificial (O Motor Invisível):** 
  * **Preditividade:** Biblioteca `Prophet` para análise de séries temporais, antecipando picos de consumo da rede com até 1h de antecedência.
  * **Comunicação/NLP:** Modelos `OpenAI` orquestrados via `LangChain` para traduzir dados brutos de energia em *insights* gerenciais diretos para o lojista.
* **Banco de Dados Estruturado:**
  * `PostgreSQL`: Dados financeiros e regras de tarifação (Garantia ACID).
  * `TimescaleDB`: Alto volume de telemetria de energia contínua.
  * `Redis`: Gestão temporária do status das sessões ativas.
* **Protocolos de Integração Base:** `MODBUS` (leitura elétrica) e `OCPP 1.6` (eventos e gestão da máquina).
* **Billing e Pagamento:** API `Abacate Pay` para geração de cobrança dinâmica via PIX.
