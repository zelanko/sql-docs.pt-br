---
title: Configurar a coleta de dados de diagnóstico e uso do SQL Server (Programa de Aperfeiçoamento da Experiência do Usuário) | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: configuration
ms.openlocfilehash: d5248f97b044cb688174171fdb6ef79943851a92
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028931"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-ceip"></a>Configurar a coleta de dados de diagnóstico e uso do SQL Server (Programa de Aperfeiçoamento da Experiência do Usuário)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="summary"></a>Resumo

Por padrão, o Microsoft SQL Server coleta informações sobre como os clientes estão usando o aplicativo. Especificamente, o SQL Server coleta informações sobre a experiência de instalação, uso e desempenho. Essas informações ajudam a Microsoft a melhorar o produto para melhor atender às necessidades do cliente. Por exemplo, a Microsoft coleta informações sobre quais tipos de códigos de erro os clientes costumam encontrar, para que possamos corrigir erros relacionados, melhorar nossa documentação sobre como usar o SQL Server e determinar se os recursos devem ser adicionados ao produto para melhor atender aos clientes.

Especificamente, a Microsoft não envia nenhum dos seguintes tipos de informações por meio desse mecanismo:
- Qualquer valor das tabelas de usuário
- Qualquer credencial de logon ou outras informações de autenticação
- Informações de Identificação Pessoal (PII)

O seguinte exemplo de cenário inclui informações de uso de recursos que ajudam a melhorar o produto.

O SQL Server 2017 tem suporte para ColumnStore para habilitar cenários de análise rápida. Os índices ColumnStore indexes combinam uma estrutura de índice "árvore B" tradicional para dados recém-inseridos a uma estrutura compactada orientada a dados especial para compactar dados e acelerar a execução das consultas. O produto contém heurística para migrar dados da estrutura de árvore B para a estrutura compactada em segundo plano, acelerando assim os futuros resultados de consulta.

Se a operação em segundo plano não acompanhar o ritmo da taxa de inserção dos dados, o desempenho da consulta pode ser mais lento do que o previsto. Para melhorar o produto, a Microsoft coleta informações sobre como o SQL Server está acompanhando o processo de compactação de dados automático. A equipe de produto usa essas informações para ajustar a frequência e paralelismo do código que executa a compactação. Essa consulta é executada, ocasionalmente, para coletar essas informações para que nós (Microsoft) possamos avaliar a taxa de movimentação de dados. Isso nos ajuda a otimizar a heurística do produto.  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

Lembre-se de que esse processo enfoca os mecanismos necessários para fornecer valor aos clientes. A equipe de produto não verifica os dados no índice nem envia esses dados para a Microsoft. O SQL Server 2017 sempre coleta e envia informações sobre a experiência de instalação do processo de configuração para que possamos localizar e corrigir rapidamente quaisquer problemas de instalação que o cliente esteja enfrentando. O SQL Server 2017 pode ser configurado para não enviar informações (em uma base de instância por servidor) para a Microsoft pelos seguintes mecanismos:
- Usando o aplicativo de Relatório de Uso e Erro
- Definindo sub-chaves de registro no servidor

Para o SQL Server no Linux, confira [Comentários de Clientes para o SQL Server no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-customer-feedback)

> [!NOTE]
> Você só pode desabilitar o envio de informações para a Microsoft em versões pagas do SQL Server.

## <a name="remarks"></a>Remarks
 - Não há suporte para remover ou desabilitar o serviço Programa de Aperfeiçoamento da Experiência do Usuário do SQL. 
 - Não há suporte para remover os recursos do Programa de Aperfeiçoamento da Experiência do Usuário do SQL do Grupo de Clusters. 

Para recusar a coleta de dados, veja [Ativando ou desativando a auditoria local](usage-and-diagnostic-data-in-local-audit.md#turning-local-audit-on-or-off)

## <a name="error-and-usage-reporting-application"></a>Aplicativo de Relatório de Uso e Erro 

Após a instalação, a configuração de coleta de dados de diagnóstico e uso para instâncias e componentes do SQL Server pode ser alterada por meio do aplicativo de Relatório de Uso e Erro. Esse aplicativo está disponível como parte da instalação do SQL Server. Essa ferramenta permite que cada instância do SQL Server defina sua própria configuração de Relatórios de Uso.

> [!NOTE]
> O aplicativo de Relatório de Uso e Erro é listado em Ferramentas de Configuração do SQL Server. Você pode usar essa ferramenta para gerenciar sua preferência para a coleta de Dados de Diagnóstico e de Uso e o Relatórios de Erro da mesma maneira do SQL Server 2017. O Relatório de Erros é separado da coleta de Dados de Diagnóstico e de Uso, portanto pode ser ativado ou desativado independentemente da coleta de Dados de Diagnóstico e de Uso. O Relatório de Erros coleta despejos de memória que são enviados à Microsoft e que podem conter informações confidenciais, conforme descrito na [Política de Privacidade](https://go.microsoft.com/fwlink/?LinkID=868444).

Para iniciar o Relatório de Uso e Erro do SQL Server, clique ou toque em **Iniciar** e pesquise "Erro" na caixa de pesquisa. O item de Relatório de Uso e Erro do SQL Server será exibido. Depois de iniciar a ferramenta, você pode gerenciar os dados de diagnóstico e uso, bem como os erros graves que são coletados para instâncias e componentes que estão instalados no computador.

Para versões pagas, use a caixa de seleção "Relatórios de Uso" para gerenciar os dados de diagnóstico e uso para a Microsoft.

Para versões pagas ou gratuitas, use a caixa de seleção "Relatórios de Erro" para gerenciar o envio de comentários sobre erros e despejos de memória para a Microsoft.

## <a name="set-registry-subkeys-on-the-server"></a>Definir a sub-chave de registro no servidor

Clientes corporativos podem definir as configurações de Política de Grupo para aceitar ou recusar a coleta de dados de diagnóstico e uso. Isso é feito com a configuração de uma política baseada no registro. As configurações e sub-chave de registro relevantes são as seguintes:

- Para recursos de instância do SQL Server:
    
    Subchave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    Nome da RegEntry = CustomerFeedback
    
    Tipo de entrada DWORD: 0 é recusar; 1 é aceitar
    
    {InstanceID} refere-se ao tipo de instância e à instância, como nos exemplos a seguir:

    - MSSQL14.CANBERRA para o mecanismo de Banco de Dados do SQL Server 2017 e nome de Instância de "CANBERRA"
    - MSAS14.CANBERRA para o SQL Server 2017 Analysis Services e nome de Instância de "CANBERRA"
    - MSRS14.CANBERRA para o SQL Server 2017 Reporting Services e nome de Instância de "CANBERRA"

- Para todos os recursos compartilhados:
    
    Subchave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Versão Principal}
    
    Nome da RegEntry = CustomerFeedback
    
    Tipo de entrada DWORD: 0 é recusar; 1 é aceitar

> [!NOTE]
> {Versão Principal} refere-se à versão do SQL Server, por exemplo, 140 para o SQL Server 2017

- Para o SQL Server Management Studio 17 e 18, confira [Assistência ao usuário no SQL Server Management Studio](../ssms/sql-server-management-studio-telemetry-ssms.md)

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>Definir as sub-chaves de registro para a coleta de despejo de memória

Semelhante ao comportamento em uma versão anterior do SQL Server, os clientes do SQL Server 2017 Enterprise podem definir as configurações de Política de Grupo para aceitar ou recusar a coleta de despejo de memória. Isso é feito com a configuração de uma política baseada no registro. As configurações e sub-chaves de registro relevantes são as seguintes: 

- Para recursos de instância do SQL Server:

    Subchave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    Nome da RegEntry = EnableErrorReporting

    Tipo de entrada DWORD: 0 é recusar; 1 é aceitar
 
    {InstanceID} refere-se ao tipo de instância e à instância, como nos exemplos a seguir: 

    - MSSQL14.CANBERRA para o mecanismo de Banco de Dados do SQL Server 2017 e nome de Instância de "CANBERRA"
    - MSAS14.CANBERRA para o SQL Server 2017 Analysis Services e nome de Instância de "CANBERRA"
    - MSRS14.CANBERRA para o SQL Server 2017 Reporting Services e nome de Instância de "CANBERRA"
 

- Para todos os recursos compartilhados:
    
    Subchave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Versão Principal}

    Nome da RegEntry = EnableErrorReporting

    Tipo de entrada DWORD: 0 é recusar; 1 é aceitar

> [!NOTE]
> {Versão Principal} refere-se à versão do SQL Server. Por exemplo, "140" refere-se ao SQL Server 2017.

A política de grupo baseada em registros nessas sub-chaves de registro é cumprida pela coleta do despejo de memória do SQL Server 2017. 

## <a name="crash-dump-collection-for-ssms"></a>Coleta de despejo de memória para o SSMS
O SSMS não coleta seu próprio despejo de memória. Nenhum despejo de memória que esteja relacionado ao SSMS é coletado como parte do Relatório de Erros do Windows.

O procedimento para ativar ou desativar este recurso depende da versão do SO. Para ativar ou desativar o recurso, siga as etapas no artigo apropriado para a sua versão do Windows.
 
- Windows Server 2016 e Windows 10

    [Configurar os dados de diagnóstico do Windows na organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)
- Windows Server 2008 R2 e Windows 7

    [Configurações WER](/windows/desktop/wer/wer-settings)
 
## <a name="feedback-for-analysis-services"></a>Comentários sobre o Analysis Services

Durante a instalação, o Analysis Services do SQL Server 2016 adiciona uma conta especial à sua instância do Analysis Services. Essa conta é um membro da função de Administrador do Servidor do Analysis Services. A conta é usada para coletar informações para comentários da instância do Analysis Services.  

Você pode configurar seu serviço para não enviar dados de diagnóstico e uso, conforme descrito na seção "Conjunto de sub-chaves do registro no servidor". No entanto, isso não removerá a conta de serviço. 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
