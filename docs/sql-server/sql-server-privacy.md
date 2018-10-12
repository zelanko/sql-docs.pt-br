---
title: Suplemento de privacidade do SQL Server | Microsoft Docs
ms.date: 4/24/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1cfb5ce2ed20788eead43c6b90a9d64378e58740
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785650"
---
# <a name="sql-server-privacy-supplement"></a>Suplemento de privacidade do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo resume o comportamento de diferentes objetos de dados usados dentro do SQL Server e como os objetos são usados para passar informações de uma maneira pessoal ou confidencial. Este artigo funciona como um adendo à [Política de privacidade geral da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839). A classificação de dados neste artigo aplica-se somente às versões do produto SQL Server local. Ela não se aplica aos itens:

- Banco de dados SQL do Azure
- SQL Server Management Studio (SSMS)
- SQL Server Data Tools (SSDT)
- Azure Data Studio
- Assistente de Migração de Banco de Dados
- Assistente de Migração do SQL Server
- Extensão do MS-SQL

Definição de *Cenários de uso permitidos*. No contexto deste artigo, a Microsoft define "Cenários de usos permitidos" como ações ou atividades que são iniciadas pela Microsoft.

## <a name="access-control"></a>Controle de acesso

Informações relacionadas a credenciais usadas para proteger logons, usuários ou contas em uma instalação do SQL Server.

### <a name="examples-of-access-control"></a>Exemplos de controle de acesso

- Senhas
- Certificados

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção |
|---------|---------|---------|
|Essas credenciais nunca saem do computador do usuário por meio de comentários de uso.     |-         |-         |
|Os despejos de memória podem conter dados de Controle de Acesso.     |-         |Despejos de memória: no máximo 30 dias.         |
|Essas credenciais nunca saem do computador do usuário por meio dos comentários de uso, a menos que o cliente as insira manualmente    |Limitado a uso interno da Microsoft sem acesso de terceiros.         |Comentários do usuário: no máximo um ano         |
 |
## <a name="customer-content"></a>Conteúdo do cliente

O conteúdo do cliente é definido como os dados armazenados em tabelas do usuário, direta ou indiretamente. Os dados incluem literais de estatísticas ou do usuário em textos de consulta que podem ser armazenados em tabelas do usuário.

### <a name="examples-of-customer-content"></a>Exemplos de conteúdo do cliente

- Valores de dados armazenados nas linhas de qualquer tabela do usuário.
- Objetos de estatísticas que contêm cópias dos valores nas linhas de qualquer tabela do usuário.
- Textos de consulta que contêm valores literais.

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos
|Cenário  |Restrições de acesso  |Requisitos de retenção |
|---------|---------|---------|
|Esses dados não saem do computador do usuário por meio de comentários de uso. |- |- |
|Os despejos de memória podem conter conteúdo do cliente e serem emitidos para a Microsoft. |- |Despejos de memória: no máximo 30 dias. |
|Mediante consentimento, os clientes podem enviar comentários do usuário que contêm conteúdo do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo um ano |

## <a name="end-user-identifiable-information-euii"></a>EUII (informações de identificação do usuário final)

Os dados recebidos de um usuário ou gerados pelo uso do produto.
- Vinculável a um usuário individual.
- Não contém conteúdo.

### <a name="examples-of-end-user-identifiable-information"></a>Exemplos de informações de identificação do usuário final

- Identificação da interface. O endereço IP completo
- Nome do computador
- Nomes de logon/usuário
- A parte local do endereço de email (joe@contoso.com)
- Informações de localização
- Identificação do cliente

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção|
|---------|---------|---------|
|Esses dados não saem do computador do usuário por meio de comentários de uso. |- |- |
|Os despejos de memória podem conter EUII e serem emitidos para a Microsoft. |- |Despejos de memória: no máximo 30 dias |
|A ID de identificação do cliente pode ser emitida para a Microsoft visando o fornecimento de novos recursos de nuvem e híbridos que o usuário tenha assinado. |- |No momento, esses tipos de recursos de nuvem ou híbridos não existem.|
|Mediante consentimento, os clientes podem enviar comentários do usuário contendo conteúdo do cliente à Microsoft.|Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo 1 ano |

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
|Mediante consentimento, os clientes podem enviar comentários do usuário que contêm conteúdo do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. |Mediante consentimento, os clientes podem enviar comentários do usuário que contêm conteúdo do cliente à Microsoft. |
|Os itens de mapeamento do Power View e do SQL Reporting Services podem enviar dados para serem usados pelo Bing Mapas. |Limitado aos dados de sessão |- |

## <a name="system-metadata"></a>Metadados do sistema

Dados gerados no decorrer da execução do servidor.  Os dados não contêm conteúdo do cliente.

### <a name="examples-of-system-metadata"></a>Exemplos de metadados do sistema

Os seguintes são considerados metadados do sistema quando não incluem cliente conteúdo de cliente, controle de acesso de cliente ou EUII:

- GUID do banco de dados
- Hash do nome do computador
- Hash do nome da instância
- Nome do aplicativo
- Dados de uso/comportamentais
- Dados do SQLCEIP (Programa de Aperfeiçoamento da Experiência do Usuário do SQL)
- Dados de configuração do servidor, por exemplo, configurações de sp_configure
- Dados de configuração de recurso
- Nomes de evento e códigos de erro

A Microsoft examina valores de nome de aplicativo definidos por outros programas que usam o SQL Server (exemplo: o Sharepoint ou programas empacotados de terceiros e inclui essas informações nos metadados do sistema enviados à Microsoft quando a opção Dados de Uso está habilitada). Os clientes não devem colocar dados pessoais, como informações de identificação do usuário final, nos campos de metadados do sistema nem criar aplicativos projetados para armazenar dados pessoais nesses campos. 

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção|
|---------|---------|---------|
|Podem ser usados pela Microsoft para melhorar recursos e/ou corrigir erros em recursos atuais.|Limitado a uso interno da Microsoft sem acesso de terceiros. |Mín. 90 dias – Máx. três anos |
|Podem ser usados para fazer sugestões ao cliente.  Por exemplo, "Com base no uso do produto, use o recurso *X* que terá um desempenho melhor". |A Microsoft pode expor os dados para o cliente original, por exemplo, por meio de painéis. |Logs de segurança de dados do cliente: mín. três anos – máx. seis anos |
Podem ser usados pela Microsoft para o planejamento futuro de produto. |A Microsoft pode compartilhar essas informações com outros fornecedores de hardware e software para melhorar a execução de seus produtos com softwares da Microsoft. |Mín. 90 dias – Máx. três anos|
|Podem ser usados pela Microsoft para fornecer serviços baseados em nuvem com base nos comentários de uso emitidos. Por exemplo, um painel de cliente mostrando o uso do recurso em todas as instalações do SQL Server em uma organização. |A Microsoft pode expor os dados para o cliente original, por exemplo, por meio de painéis. |Mín. 90 dias – Máx. três anos |
|Mediante consentimento, os clientes podem enviar comentários do usuário que contêm conteúdo do cliente à Microsoft. |Limitado a uso interno da Microsoft sem acesso de terceiros. A Microsoft pode expor os dados para o cliente original. |Comentários do usuário: no máximo um ano |
|A Microsoft pode usar o nome do banco de dados e o nome do aplicativo para categorizar bancos de dados e aplicativos, como aqueles que possam estar executando algum software fornecido pela Microsoft ou por outras empresas, em categorias conhecidas.|Limitado a uso interno da Microsoft sem acesso de terceiros.|Mín. 90 dias – Máx. três anos |

## <a name="object-metadata"></a>Metadados de objeto

Dados que descrevem ou são usados para configurar servidores, bancos de dados, tabelas e outros recursos.  Os metadados de objeto incluem nomes de coluna e tabela de banco de dados, mas não o conteúdo das linhas do banco de dados nem outro conteúdo do cliente. Os clientes não devem colocar dados pessoais, como informações de identificação do usuário final nos campos de metadados de objeto nem criar aplicativos projetados para armazenar dados pessoais nesses campos. Para o cenário de uso permitido abaixo, apenas o formulário de hash é usado para determinar os padrões de uso para melhorar o produto. 

### <a name="examples-of-object-metadata"></a>Exemplos de metadados de objeto

- Nomes de banco de dados do SQL Server
- Nomes de tabela e nomes de coluna
- Nomes de estatísticas

### <a name="permitted-usage-scenarios"></a>Cenários de uso permitidos

|Cenário  |Restrições de acesso  |Requisitos de retenção|
|---------|---------|---------|
|Podem ser usados pela Microsoft para melhorar recursos e/ou corrigir erros em recursos atuais. |Limitado a uso interno da Microsoft sem acesso de terceiros. |Mín. 90 dias – Máx. três anos|

## <a name="telemetry-controls"></a>Controles de telemetria

As instruções de como a telemetria pode ser habilitada/desabilitada no produto podem ser encontradas aqui: https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
