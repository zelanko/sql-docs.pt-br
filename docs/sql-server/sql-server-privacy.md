---
description: Suplemento de privacidade do SQL Server
title: Suplemento de privacidade do SQL Server | Microsoft Docs
ms.date: 11/11/2020
ms.prod: sql
ms.technology: release-landing
ms.reviewer: wopeter
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 87cd9ec5266002f91fea682591e82dfecd403ab5
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549998"
---
# <a name="sql-server-privacy-supplement"></a>Suplemento de privacidade do SQL Server

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

Este artigo resume os recursos habilitados para Internet que podem coletar e enviar os dados anônimos de diagnóstico e uso de recursos à Microsoft. O SQL Server pode coletar informações padrão do computador e dados de uso e desempenho que podem ser transmitidas à Microsoft e analisadas com a finalidade de aprimorar a qualidade, a segurança e a confiabilidade do produto. Se você instalar o SQL Server em uma máquina virtual no serviço do Microsoft Azure, as informações do ambiente poderão ser enviadas à Microsoft para que ela possa instalar a Extensão do Agente de IaaS do SQL Server e registrar seu recurso de máquina virtual no provedor de recursos de VM SQL, conforme descrito [aqui](/azure/azure-sql/virtual-machines/windows/sql-vm-resource-provider-register).

Este artigo funciona como um adendo à [Política de privacidade geral da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839). A classificação de dados neste artigo aplica-se somente às versões do produto SQL Server local. Ela não se aplica aos itens:

- Banco de Dados SQL do Azure
- [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-telemetry-ssms.md)
- SSDT (SQL Server Data Tools)
- Azure Data Studio
- Assistente de Migração de Dados
- Assistente de Migração do SQL Server
- Extensão do MS-SQL

Definição de *Cenários de uso permitidos*. No contexto deste artigo, a Microsoft define "Cenários de usos permitidos" como ações ou atividades que são iniciadas pela Microsoft.

## <a name="access-control"></a>Controle de acesso

Informações relacionadas a credenciais usadas para proteger logons, usuários ou contas em uma instalação do SQL Server.

### <a name="examples-of-access-control"></a>Exemplos de controle de acesso

- Senhas
- Certificados

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário |Restrições de acesso |Requisitos de retenção |
|---------|---------|---------|
|Essas credenciais nunca saem do computador do usuário por meio de Dados de Uso e Diagnóstico. |- |- |
|Os despejos de memória podem conter dados de Controle de Acesso. |- |Despejos de memória: no máximo 30 dias. |
|Essas credenciais nunca saem do computador do usuário por meio dos comentários de uso, a menos que o cliente as insira manualmente |Limitado a uso interno da Microsoft sem acesso de terceiros. |Comentários do usuário: no máximo um ano|
|&nbsp;|&nbsp;|&nbsp;|

## <a name="customer-data"></a>Dados do cliente

Os dados do cliente são definidos como os dados armazenados em tabelas do usuário, direta ou indiretamente. Os dados incluem literais de estatísticas ou do usuário em textos de consulta que podem ser armazenados em tabelas do usuário.

### <a name="examples-of-customer-data"></a>Exemplos de dados do cliente

- Valores de dados armazenados nas linhas de qualquer tabela do usuário.
- Objetos de estatísticas que contêm cópias dos valores nas linhas de qualquer tabela do usuário.
- Textos de consulta que contêm valores literais.

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção |
|---------|---------|---------|
|Esses dados não saem do computador do usuário por meio de Dados de Uso e Diagnóstico. |- |- |
|Os despejos de memória podem conter dados do cliente e ser emitidos para a Microsoft. |- |Despejos de memória: no máximo 30 dias. |
|Mediante consentimento, os clientes podem enviar comentários do usuário contendo dados do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo um ano |

## <a name="personal-data"></a>Dados pessoais

Os dados recebidos de um usuário ou gerados pelo uso do produto.
- Vinculável a um usuário individual.
- Não contém dados do cliente.

### <a name="examples-of-personal-data"></a>Exemplos de dados pessoais

- Identificação da interface. O endereço IP completo
- Nome do computador
- Nomes de logon/usuário
- A parte local do endereço de email (joe@contoso.com)
- Informações de localização
- Identificação do cliente

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção|
|---------|---------|---------|
|Esses dados não saem do computador do usuário por meio de Dados de Uso e Diagnóstico. |- |- |
|Os despejos de memória podem conter dados pessoais e ser emitidos para a Microsoft. |- |Despejos de memória: no máximo 30 dias |
|A ID de identificação do cliente pode ser emitida para a Microsoft visando o fornecimento de novos recursos de nuvem e híbridos que o usuário tenha assinado. |- |No momento, esses tipos de recursos de nuvem ou híbridos não existem.|
|Mediante consentimento, os clientes podem enviar comentários do usuário contendo dados do cliente à Microsoft.|Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo 1 ano |

## <a name="internet-based-services-data"></a>Dados de serviços baseados na Internet

Dados necessários para fornecer serviços baseados na Internet, de acordo com os termos de licença do SQL Server.

### <a name="examples-of-internet-based-services-data"></a>Exemplos de dados de serviços baseados na Internet

- Informações de especificação do computador
- Nome/versão do navegador
- Versão do SQL Server
- Código de idioma
- Um endereço IP com determinados octetos removidos
- Dados de mapa

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção|
|---------|---------|---------| 
|Podem ser usados pela Microsoft para melhorar recursos e/ou corrigir erros em recursos atuais. |Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original.  Por exemplo, os painéis |Mín. 90 dias – Máx. três anos |
|Mediante consentimento, os clientes podem enviar comentários do usuário contendo dados do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. |Mediante consentimento, os clientes podem enviar comentários do usuário contendo dados do cliente à Microsoft. |
|Os itens de mapeamento do Power View e do SQL Reporting Services podem enviar dados para serem usados pelo Bing Mapas. |Limitado aos dados de sessão |- |

## <a name="non-personal-data"></a>Dados não pessoais

1. Os dados recebidos de uma organização ou gerados pelo uso do produto. Eles são vinculáveis a uma organização e não contêm dados do cliente.

   - Exemplo
     - Nome da organização (exemplo: Microsoft Corp.)

   - Cenários de uso permitidos

     |Cenário  |Restrições de acesso  |Requisitos de retenção|
     |---------|---------|---------|
     | A Microsoft pode coletar dados de uso genéricos de instâncias do SQL Server em execução em Máquinas Virtuais do Azure para a finalidade expressa de fornecer aos clientes benefícios opcionais no Azure para usar SQL Server em Máquinas Virtuais do Azure. | A Microsoft pode expor dados ao cliente, por exemplo, por meio do portal do Azure, para ajudar os clientes que executam SQL Server em Máquinas Virtuais do Azure a acessar os benefícios específicos da execução do SQL Server no Azure. </br></br>A Microsoft não usará esses dados para auditorias de licenciamento sem o consentimento antecipado do cliente. | Mín. 90 dias – Máx. três anos |

2. Dados que descrevem ou são usados para configurar servidores, bancos de dados, tabelas e outros recursos criados ou fornecidos por clientes. Eles incluem nomes de coluna e tabela de banco de dados, mas não o conteúdo das linhas do banco de dados nem outros dados do cliente. Os clientes não devem colocar dados pessoais nesses campos de metadados do sistema nem criar aplicativos projetados para armazenar dados pessoais nesses campos. Nos cenários de uso permitido abaixo, apenas o formulário de hash é usado a fim de determinar os padrões de uso para melhorar o produto.

   - Exemplo
      - Nomes de banco de dados do SQL Server
      - Nomes de tabela e nomes de coluna
      - Nomes de estatísticas

    - Cenários de uso permitidos

      > [!NOTE]
      > Todos os valores de metadados são transformados em hash antes da coleção.
      >

      |Cenário  |Restrições de acesso  |Requisitos de retenção|
      |---------|---------|---------|
      |Podem ser usados pela Microsoft para melhorar recursos e/ou corrigir erros em recursos atuais. |Limitado a uso interno da Microsoft sem acesso de terceiros. |Mín. 90 dias – Máx. três anos|

3. Dados gerados no decorrer da execução do servidor. Eles não contém dados do cliente, dados não pessoais, como listados em 1. ou 2. (acima), dados de controle de acesso do cliente ou dados pessoais.

   - Exemplo
     - GUID do banco de dados
     - Hash do nome do computador
     - Hash do nome da instância
     - Nome do aplicativo
     - Dados de uso/comportamentais
     - Dados do SQLCEIP (Programa de Aperfeiçoamento da Experiência do Usuário do SQL)
     - Dados de configuração do servidor, por exemplo, configurações de sp_configure
     - Dados de configuração de recurso
     - Nomes de evento e códigos de erro
     - Configurações e identificação de hardware, como o fabricante OEM

   A Microsoft examina os valores de nome de aplicativo definidos por outros programas que usam o SQL Server (exemplo: SharePoint ou programas de terceiros) e inclui essas informações nos campos de metadados enviados à Microsoft quando os Dados de Uso estão habilitados. Os clientes não devem colocar dados pessoais nesses campos de metadados do sistema nem criar aplicativos projetados para armazenar dados pessoais nesses campos.

   - Cenários de uso permitidos

     |Cenário  |Restrições de acesso  |Requisitos de retenção|
     |---------|---------|---------|
     |Podem ser usados pela Microsoft para melhorar recursos e/ou corrigir erros em recursos atuais.|Limitado a uso interno da Microsoft sem acesso de terceiros. |Mín. 90 dias – Máx. três anos |
     |Podem ser usados para fazer sugestões ao cliente.  Por exemplo, "Com base no uso do produto, use o recurso *X* que terá um desempenho melhor". |A Microsoft pode expor os dados para o cliente original, por exemplo, por meio de painéis. |Logs de segurança de dados do cliente: mín. três anos – máx. seis anos |
     |Podem ser usados pela Microsoft para o planejamento futuro de produto. |A Microsoft pode compartilhar essas informações com outros fornecedores de hardware e software para melhorar a execução de seus produtos com softwares da Microsoft. |Mín. 90 dias – Máx. três anos|
     |Podem ser usados pela Microsoft para fornecer serviços baseados em nuvem com base nos Dados de Diagnóstico e Uso emitidos. Por exemplo, um painel de cliente mostrando o uso do recurso em todas as instalações do SQL Server em uma organização. |A Microsoft pode expor os dados para o cliente original, por exemplo, por meio de painéis. |Mín. 90 dias – Máx. três anos |
     |Mediante consentimento, os clientes podem enviar comentários do usuário contendo dados do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo um ano |
     |A Microsoft pode usar o nome do banco de dados e o nome do aplicativo para categorizar bancos de dados e aplicativos, como aqueles que possam estar executando algum software fornecido pela Microsoft ou por outras empresas, em categorias conhecidas.|Limitado a uso interno da Microsoft sem acesso de terceiros.|Mín. 90 dias – Máx. três anos |

## <a name="system-generated-logs-controls"></a>Controles de logs gerados pelo sistema

As instruções sobre como os logs gerados pelo sistema podem ser ativados/desativados no produto podem ser consultadas aqui: [Configurar a coleta de dados de diagnóstico e uso do SQL Server (Programa de Aperfeiçoamento da Experiência do Usuário)](usage-and-diagnostic-data-configuration-for-sql-server.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
