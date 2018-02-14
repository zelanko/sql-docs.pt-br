---
title: Ajuda F1 do Visualizador do Arquivo de Log | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63be87acc6f5ef1f550f7ec9d03cad7eab93e6a6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="log-file-viewer-f1-help"></a>Ajuda F1 do Visualizador do Arquivo de Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O Visualizador do Arquivo de Log exibe informações de muitos componentes diferentes. Quando o Visualizador do Arquivo de Log estiver aberto, use o painel **Selecionar logs** para selecionar os logs que deseja exibir. Cada log exibe as colunas adequadas àquele tipo de log.  
  
 Os logs disponíveis dependem de como o Visualizador do Arquivo de Log é aberto. Para obter mais informações, consulte [Abrir o Visualizador do Arquivo de Log](../../relational-databases/logs/open-log-file-viewer.md).  
  
 O número de linhas exibidas para logs de auditoria pode ser configurado na página **Pesquisador de Objetos do SQL Server/Comandos** da caixa de diálogo **Ferramentas/Opções**. Para obter descrições das colunas exibidas para logs de auditoria, consulte [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md).  
  
## <a name="options"></a>Opções  
 **Carregar Log**  
 Abra uma caixa de diálogo onde seja possível especificar um arquivo de log a ser carregado.  
  
 **Exportar**  
 Abra uma caixa de diálogo que permita exportar as informações mostradas na grade **Resumo do arquivo de log** para um arquivo de texto.  
  
 **Atualizar**  
 Atualize a exibição dos logs selecionados. O botão **Atualizar** relê os logs selecionados do servidor de destino ao aplicar qualquer configuração de filtro.  
  
 **Filtro**  
 Abra uma caixa de diálogo que permita especificar configurações usadas para filtrar o arquivo de log, como **Conexão**, **Data**ou outros critérios de filtragem **Gerais** .  
  
 **Pesquisa**  
 Pesquise o texto específico no arquivo de log. Não há suporte à pesquisa com caracteres curinga.  
  
 **Parar**  
 Interrompe o carregamento das entradas do arquivo de log. Por exemplo, você poderá usar essa opção se um arquivo de log remoto ou offline demorar muito tempo para ser carregado e você desejar exibir apenas as entradas mais recentes.  
  
 **Resumo do arquivo de log**  
 Esse painel de informações exibe um resumo da filtragem do arquivo de log. Se o arquivo não for filtrado, você verá o seguinte texto, **Nenhum filtro aplicado**. Se um filtro for aplicado ao log, você verá o seguinte texto **Filtrar entradas do log, em que:**  \<filter criteria>.  
  
 **Detalhes da linha selecionada**  
 Selecione uma linha para exibir detalhes adicionais sobre a linha de evento selecionada na parte inferior da página. As colunas podem ser reordenadas arrastando-as para locais novos na grade. As colunas podem ser redimensionadas arrastando para a esquerda ou direta as barras separadoras de coluna no cabeçalho de grade. Clique duas vezes nas barras separadoras de coluna no cabeçalho da grade para dimensionar automaticamente a coluna para a largura do conteúdo.  
  
 **Instância**  
 O nome da instância do na qual ocorreu o evento. Esse nome é exibido como *nome do computador*\\*nome da instância*.  
  
## <a name="frequently-displayed-columns"></a>Colunas exibidas frequentemente  
 **Data**  
 Exibe a data do evento.  
  
 **Origem**  
 Exibe o recurso de origem do qual o evento é criado, como o nome do serviço (MSSQLSERVER, por exemplo). Isso não é exibido para todos os tipos de log.  
  
 **Mensagem**  
 Exibe todas as mensagens associadas ao evento.  
  
 **Tipo de Log**  
 Exibe o tipo de log ao qual o evento pertence. Todos os logs selecionados são exibidos na janela de resumo de arquivo de log.  
  
 **Origem do Log**  
 Exibe uma descrição do log de origem no qual o evento é capturado.  
  
## <a name="permissions"></a>Permissões  
 Para acessar arquivos de log de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão online, é necessária associação na função de servidor fixa securityadmin.  
  
 Para acessar arquivos de log de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão offline, é necessário ter acesso de leitura no namespace do WMI **Root\Microsoft\SqlServer\ComputerManagement10** e na pasta em que os arquivos de log estão armazenados. Para obter mais informações, veja a seção Segurança do tópico [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer.md)   
 [Abrir o Visualizador do Arquivo de Log](../../relational-databases/logs/open-log-file-viewer.md)   
 [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
