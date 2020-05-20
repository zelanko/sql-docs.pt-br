---
title: Elemento de carga de trabalho (DTA)
description: No utilitário dta, o elemento Workload especifica a carga de trabalho a ser usada em uma sessão de ajuste. Este artigo descreve esse elemento.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 5ac7f5a55ce968eeb2ca274deff09ff8b7f2e4ae
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151464"
---
# <a name="workload-element-dta"></a>Elemento de carga de trabalho (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica a carga de trabalho a ser usada em uma sessão de ajuste.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Necessário uma vez para cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**Elementos filho**|[Elemento File &#40;DTA&#41;](../../tools/dta/file-element-dta.md)<br /><br /> [Elemento Database para Workload &#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)<br /><br /> [Elemento EventString &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. O Orientador de Otimização do Mecanismo de Banco de Dados pode usar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , arquivos de rastreamento e tabelas de rastreamento como cargas de trabalho.  
  
 Se você especificar uma carga de trabalho em arquivo de entrada XML e uma carga de trabalho na linha de comando com a ferramenta **dta** , a carga de trabalho especificada na linha de comando será usada para ajuste. Todas as opções de ajuste especificadas na linha de comando substituem as que foram especificadas no arquivo de entrada XML. A única exceção será se uma configuração especificada pelo usuário for digitada dentro do modo de avaliação no arquivo de entrada XML. Por exemplo, se a configuração digitada no elemento **Configuration** do arquivo de entrada XML do elemento **EvaluateConfiguration** também for especificada como uma das opções de ajuste, as opções de ajuste especificadas no arquivo de entrada XML substituirão todas as opções de ajuste da linha de comando.  
  
 É preciso especificar uma carga de trabalho para cada sessão de ajuste.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica o arquivo de rastreamento **MyDatabase.MyDBOwner.TuningTable001** para o elemento **Workload** . A **TuningTable001** foi criada usando-se do modelo de ajuste com o SQL Server Profiler e salvando a saída do rastreamento como tabela.  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
