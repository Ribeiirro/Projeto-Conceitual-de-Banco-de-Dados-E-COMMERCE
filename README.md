# 🚗 Sistema de Gestão de Ordem de Serviço - Oficina Mecânica

## 📌 Descrição do Projeto

Este projeto apresenta um modelo conceitual para um sistema de gerenciamento de ordens de serviço em uma **oficina mecânica**. A proposta inclui o controle de **clientes**, **veículos**, **mecânicos**, **serviços**, **peças**, **pagamentos** e **entregas**. O modelo foi estendido com os seguintes pontos:

### 🔧 Refinamentos Aplicados

- **Cliente PF e PJ**: Um cliente pode ser pessoa física ou jurídica, mas não ambos.
- **Pagamento**: Uma OS pode ter múltiplas formas de pagamento associadas.
- **Entrega**: Agora há controle de status e código de rastreio da entrega associada a uma OS.

## 📊 Modelo Conceitual (ERD)

O modelo conceitual está representado em Mermaid, diretamente abaixo:

```mermaid
erDiagram

    CLIENTE ||--o{ VEICULO : possui
    CLIENTE {
        int id_cliente
        string nome
        string telefone
        string endereco
    }

    CLIENTE ||--|| CLIENTE_PF : eh
    CLIENTE_PF {
        string cpf
        date data_nascimento
    }

    CLIENTE ||--|| CLIENTE_PJ : eh
    CLIENTE_PJ {
        string cnpj
        string razao_social
    }

    VEICULO ||--o{ ORDEM_SERVICO : pertence
    VEICULO {
        int id_veiculo
        string placa
        string modelo
        string marca
        int ano
    }

    EQUIPE ||--o{ ORDEM_SERVICO : executa
    EQUIPE {
        int id_equipe
        string nome_equipe
    }

    EQUIPE ||--o{ MECANICO : composta_por
    MECANICO {
        int id_mecanico
        string nome
        string endereco
        string especialidade
    }

    ORDEM_SERVICO {
        int numero_os
        date data_emissao
        date data_conclusao
        float valor_total
        string status
        boolean autorizada
    }

    ORDEM_SERVICO ||--o{ OS_SERVICO : contem
    SERVICO ||--o{ OS_SERVICO : descrito_em
    SERVICO {
        int id_servico
        string descricao
        float valor_mao_obra
    }

    ORDEM_SERVICO ||--o{ OS_PECA : usa
    PECA ||--o{ OS_PECA : utilizada_em
    PECA {
        int id_peca
        string descricao
        float valor_unitario
    }

    OS_SERVICO {
        int quantidade
    }

    OS_PECA {
        int quantidade
    }

    ORDEM_SERVICO ||--o{ PAGAMENTO : possui
    PAGAMENTO {
        int id_pagamento
        string forma_pagamento
        float valor
        date data_pagamento
    }

    ORDEM_SERVICO ||--|| ENTREGA : possui
    ENTREGA {
        int id_entrega
        string status
        string codigo_rastreio
    }

