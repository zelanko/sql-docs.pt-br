---
description: Definição de dados MDX – CREATE ACTION
title: CRIAR instrução de ação (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7132c28e93dbc11eee1c5a4e4d53126f280fa74a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494899"
---
# <a name="mdx-data-definition---create-action"></a>Definição de dados MDX – CREATE ACTION


  Cria uma ação que pode ser associada a um cubo, uma dimensão, uma hierarquia ou um objeto subordinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma cadeia de caracteres válida que fornece um nome de cubo.  
  
 *Nome do Action_*  
 Uma cadeia de caracteres válida que fornece o nome da ação que está sendo criada.  
  
 *Nome do Hierarchy_*  
 Uma cadeia de caracteres válida que fornece um nome de hierarquia.  
  
 *Nome do Level_*  
 Uma cadeia de caracteres válida que fornece um nome de nível.  
  
 *Nome do Member_*  
 Uma cadeia de caracteres válida que fornece um nome ou chave de membro.  
  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida.  
  
## <a name="remarks"></a>Comentários  
 Os aplicativos cliente podem criar e executar ações que não são seguras, além de usar funções que não são seguras. Para evitar essas situações, use a propriedade **Opções de segurança** . Para obter mais informações, consulte as Propriedade de Opções de Segurança.  
  
> [!NOTE]  
>  Esta instrução é incluída para compatibilidade com versões anteriores. Não há suporte para ações novas para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , como ações de detalhamento ou de relatório.  
  
## <a name="action-types"></a>Tipos de ação  
 A tabela a seguir descreve os diferentes tipos de ações disponíveis no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo de ação|Descrição|  
|-----------------|-----------------|  
|**URL**|A cadeia de caracteres de ação retornada é uma URL que deve ser aberto usando um navegador de Internet.<br /><br /> Observação: se essa ação não iniciar com `https://` ou `https://` , a ação não estará disponível para o navegador, a menos que **SafetyOptions** esteja definido como **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|A cadeia de caracteres de ação retornada é um script HTML. A cadeia de caracteres deve ser salva em um arquivo e o arquivo deve ser processado com um navegador de Internet. Neste caso, um script inteiro pode ser executado como parte do HTML gerado.|  
|**PRIVACIDADE**|A cadeia de caracteres de ação retornada é uma instrução que precisa ser executada definindo o método **ICommand:: SetText** de um objeto de comando para a cadeia de caracteres e chamando o método **ICommand:: execute**. Se o comando não tiver êxito, um erro será retornado.|  
|**DATASET**|A cadeia de caracteres de ação retornada é uma instrução MDX que precisa ser executada definindo o método **ICommand:: SetText** de um objeto de comando para a cadeia de caracteres e chamando o método **ICommand:: execute** . A ID de interface solicitada (IID) deve ser **IDataset**. O comando terá êxito se um conjunto de dados tiver sido criado. O aplicativo cliente deve permitir que o usuário navegue pelo conjunto de dados retornado.|  
|**LINHAS**|Semelhante ao **DataSet**, mas em vez de solicitar um IID de **IDataset**, o aplicativo cliente deve solicitar um IID de **IRowset**. O comando terá êxito se um conjunto de linhas tiver sido criado. O aplicativo cliente deve permitir que o usuário navegue pelo conjunto de linhas retornado.|  
|**COMMANDLINE**|O aplicativo cliente deve executar a cadeia de caracteres de ação. A cadeia de caracteres é uma linha de comando.|  
|**PRÓPRIO**|O aplicativo cliente não deve exibir nem executar a ação, a não ser que o aplicativo tenha um conhecimento personalizado e não genérico da ação específica. As ações proprietárias não são retornadas ao aplicativo cliente, a menos que o aplicativo cliente solicite explicitamente isso definindo a restrição apropriada no **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Tipos de invocação  
 A tabela a seguir descreve os diferentes tipos de invocação disponíveis no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O tipo de invocação é usado somente pelo aplicativo cliente para ajudar a determinar quando a ação deve ser invocada. O tipo de invocação não determina realmente o comportamento de invocação da ação.  
  
|Tipo de invocação|Descrição|  
|---------------------|-----------------|  
|**INTERACTIVE**|A ação deve ser invocada pelo aplicativo cliente por meio da interação do usuário.|  
|**ON_OPEN**|A ação deve ser invocada pelo aplicativo cliente quando o objeto de destino é aberto. Esse tipo de invocação não é implementado atualmente.|  
|**LOTE**|A ação deve ser invocada pelo aplicativo cliente quando o objeto de destino é envolvido em uma operação em lotes, conforme determinado pelo aplicativo cliente. Esse tipo de invocação não é implementado atualmente.|  
  
### <a name="scope"></a>Escopo  
 Cada ação é definida para um cubo específico e tem um nome exclusivo nesse cubo. Uma ação pode ter um dos escopos listados na tabela a seguir.  
  
 Escopo de cubo  
 Para ações independentes de dimensões, membros ou células específicos; por exemplo, “Lançar emulação terminal para o sistema de produção AS/400”.  
  
 Escopo de dimensão  
 A ação se aplica a uma dimensão específica. Essas ações não dependem da seleção específica de níveis ou membros.  
  
 Escopo de nível  
 A ação se aplica a um nível de dimensão específico. Essas ações não dependem da seleção específica de um membro dessa dimensão.  
  
 Escopo de membro  
 A ação se aplica a membros de nível específicos.  
  
 Escopo de célula  
 A ação se aplica somente a células específicas.  
  
 Escopo de conjunto  
 A ação se aplica somente a um conjunto. O nome, **ActionParameterSet**, é reservado para uso pelo aplicativo dentro da expressão da ação.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
