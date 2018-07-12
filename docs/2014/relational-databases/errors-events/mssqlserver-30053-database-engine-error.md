---
title: MSSQLSERVER_30053 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8ad23889-e243-4bd7-bc3e-150403399d89
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9104dc7cb2a569061760acacdbbc385e10b1f817
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412501"
---
# <a name="mssqlserver30053"></a>MSSQLSERVER_30053
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|30053|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|Texto da mensagem|Foi atingido o tempo limite de quebra de palavras para a cadeia de consulta de texto completo. O separador de palavras pode ter demorado para processar a cadeia de consulta de texto completo ou um grande número de consultas está em execução no servidor. Tente executar a consulta novamente com uma carga mais leve.|  
  
## <a name="explanation"></a>Explicação  
 Um erro de tempo limite na separação de palavras pode ocorrer nas seguintes situações:  
  
-   O separador de palavras para o idioma da consulta está configurado incorretamente. Por exemplo, suas configurações de Registro estão incorretas.  
  
-   O separador de palavras funciona incorretamente em uma cadeia de consulta específica.  
  
-   O separador de palavras retorna uma quantidade excessiva de dados para uma cadeia de consulta específica. O excesso de dados é tratado como um ataque de saturação de buffer em potencial e desliga o processo de daemon de filtro (fdhost.exe) que hospeda os serviços de separação de palavras.  
  
-   A configuração do processo de daemon de filtro está incorreta.  
  
     A maior parte dos problemas comuns de configuração são vencimento de senha ou uma política de domínio que impede que a conta do daemon do filtro faça o logon.  
  
-   Uma carga de trabalho de consultas muito pesada está em execução na instância do servidor. Por exemplo, o separador de palavras demorou muito para processar a cadeia de consultas de texto completo ou um grande número de consultas está em execução no servidor. Observe que essa é a causa menos provável.  
  
## <a name="user-action"></a>Ação do usuário  
 Selecione a ação do usuário apropriada à causa provável do tempo limite, da seguinte maneira:  
  
|Causa provável|Ação do usuário|  
|--------------------|-----------------|  
|O separador de palavras para o idioma da consulta está configurado incorretamente.|Se você estiver usando um separador de palavras de terceiros, ele poderá estar registrado incorretamente com o sistema operacional. Nesse caso, registre novamente o separador de palavras. Para obter mais informações, consulte [Reverter os separadores de palavras usados pela pesquisa para a versão anterior](../search/revert-the-word-breakers-used-by-search-to-the-previous-version.md).|  
|O separador de palavras funciona incorretamente em uma cadeia de consulta específica.|Se o separador de palavras for suportado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entre em contato com o Suporte e Atendimento ao Cliente Microsoft.|  
|O separador de palavras retorna uma quantidade excessiva de dados para uma cadeia de consulta específica.|Se o separador de palavras for suportado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entre em contato com o Suporte e Atendimento ao Cliente Microsoft.|  
|A configuração do processo de daemon de filtro está incorreta.|Verifique se você está usando a senha atual e se uma política de domínio não está impedindo a conta do daemon de filtro de fazer logon.|  
|Uma carga de trabalho de consulta muito pesada está em execução na instância do servidor.|Tente executar a consulta novamente com uma carga mais leve.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Pesquisa de Texto Completo](../search/full-text-search.md)   
 [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)   
 [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar filtros de pesquisa](../search/configure-and-manage-filters-for-search.md)  
  
  
