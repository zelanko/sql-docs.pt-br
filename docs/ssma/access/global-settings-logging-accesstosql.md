---
title: Configurações globais (log) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 835b09b5-eb42-47ea-b46e-e115d4d6461f
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c03a187baaec0f98aeb0b8f95863423a63894947
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-logging-accesstosql"></a>Configurações globais (log) (AccessToSQL)
Use o **configurações globais** caixa de diálogo para especificar as configurações de log para o SSMA. Normalmente, altere essas configurações apenas ao trabalhar com o suporte ao produto.  
  
Para acessar essa caixa de diálogo, no **ferramentas** menu, selecione **configurações globais** e, em seguida, clique no **log** botão na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Nível de mensagens**  
As seguintes opções estão disponíveis em **nível mensagens**:  
  
|Opção|Description|  
|----------|---------------|  
|**[todas as categorias]**|Usado para definir o nível de log para todas as opções a seguir.|  
|**Coletor**|Metadados sobre o esquema de origem de coleta e salva-o ao projeto.|  
|**Conversor**|Converte a estruturas de objetos de banco de dados de origem, como tabelas e procedimentos armazenados, em correspondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] estruturas.|  
|**Migrator de dados**|Migra os dados do banco de dados de origem em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Formatador**|Subcomponente do conversor que gera scripts para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema.|  
|**Interface gráfica do usuário**|Mensagens que aparecem quando você usar a ferramenta SSMA.|  
|**Vinculador**|Resolve os identificadores SQL e fornece informações para outros componentes.|  
|**Outro**|Todas as mensagens que não estão em qualquer outra categoria.|  
|**Analisador**|Analisa o esquema de origem.|  
|**Sincronizador**|Objetos de banco de dados da fonte de cargas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**TreeConverter**|Converte objetos em uma fonte de metadados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados.|  
  
Para cada opção em **mensagens nível**, configure um dos seguintes níveis de log para o SSMA:  
  
|||  
|-|-|  
|**Erro fatal**|Grave somente mensagens de erro fatal no log.|  
|**Erro**|Grave no log de erro e mensagens de erro fatal.|  
|**Aviso**|Grave mensagens de erro fatal, de aviso e erro no log.|  
|**informações de**|Gravação informativos, de aviso, erro e mensagens de erro fatal para o log.|  
|**Depurador**|Grave todas as mensagens, incluindo mensagens, o log de depuração.|  
  
**Caminho do arquivo de log**  
O caminho do arquivo e o nome dos arquivos de log SSMA. Para especificar um nome diferente, clique no caminho atual e, em seguida, clique no botão Procurar (**...** ) botão.  
  
**Tamanho do arquivo de log**  
O tamanho máximo do arquivo de log em KB. O tamanho mínimo é de 10 KB. O tamanho padrão é 10240 KB.  
  
**Número total de arquivos de log**  
Quando um log ficar cheio, o SSMA renomear o arquivo de log e iniciar um novo. Usando essa configuração, especifique o número máximo de arquivos de log para manter. O mínimo é 2.  
  
