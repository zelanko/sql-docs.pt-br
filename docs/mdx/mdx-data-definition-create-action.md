---
title: "Instrução CREATE ACTION (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ACTION
- Action
- CREATE
- CREATE_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- invocation types [MDX]
- dimensions [Analysis Services], actions
- CREATE ACTION statement
- cubes [Analysis Services], actions
- actions [MDX]
- hierarchies [Analysis Services], actions
ms.assetid: 0419f349-ece2-42ba-8552-a1023f268a41
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 195d9b9d166838a98f9e5c11e10aa9557c8ad0c6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-action"></a>Definição de dados MDX - Criar ação
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 *Nome de Action_*  
 Uma cadeia de caracteres válida que fornece o nome da ação que está sendo criada.  
  
 *Nome de Hierarchy_*  
 Uma cadeia de caracteres válida que fornece um nome de hierarquia.  
  
 *Nome de Level_*  
 Uma cadeia de caracteres válida que fornece um nome de nível.  
  
 *Nome de Member_*  
 Uma cadeia de caracteres válida que fornece um nome ou chave de membro.  
  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida.  
  
## <a name="remarks"></a>Comentários  
 Os aplicativos cliente podem criar e executar ações que não são seguras, além de usar funções que não são seguras. Para evitar essas situações, use o **Safety Options** propriedade. Para obter mais informações, consulte as Propriedade de Opções de Segurança.  
  
> [!NOTE]  
>  Esta instrução é incluída para compatibilidade com versões anteriores. As novas ações para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], como ações de detalhamento ou relatório, não têm suporte.  
  
## <a name="action-types"></a>Tipos de ação  
 A tabela a seguir descreve os diferentes tipos de ações disponíveis no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Tipo de ação|Description|  
|-----------------|-----------------|  
|**URL**|A cadeia de caracteres de ação retornada é uma URL que deve ser aberto usando um navegador de Internet.<br /><br /> Observação: Se essa ação não começar com `http://` ou `https://`, a ação estará disponível para o navegador, a menos que **SafetyOptions** é definido como **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|A cadeia de caracteres de ação retornada é um script HTML. A cadeia de caracteres deve ser salva em um arquivo e o arquivo deve ser processado com um navegador de Internet. Neste caso, um script inteiro pode ser executado como parte do HTML gerado.|  
|**INSTRUÇÃO**|A cadeia de caracteres de ação retornada é uma instrução que precisa ser executada definindo o **ICommand::SetText** método de um objeto de comando para a cadeia de caracteres e chamar o **ICommand:: execute**método. Se o comando não tiver êxito, um erro será retornado.|  
|**CONJUNTO DE DADOS**|A cadeia de caracteres de ação retornada é uma instrução MDX que precisa ser executada definindo o **ICommand::SetText** método de um objeto de comando para a cadeia de caracteres e chamar o **ICommand:: execute** método. A interface solicitada IID (ID) deve ser **IDataset**. O comando terá êxito se um conjunto de dados tiver sido criado. O aplicativo cliente deve permitir que o usuário navegue pelo conjunto de dados retornado.|  
|**CONJUNTO DE LINHAS**|Semelhante ao **DATASET**, mas em vez de solicitar uma IID de **IDataset**, o aplicativo cliente deve solicitar uma IID de **IRowset**. O comando terá êxito se um conjunto de linhas tiver sido criado. O aplicativo cliente deve permitir que o usuário navegue pelo conjunto de linhas retornado.|  
|**LINHA DE COMANDO**|O aplicativo cliente deve executar a cadeia de caracteres de ação. A cadeia de caracteres é uma linha de comando.|  
|**PROPRIETÁRIOS**|O aplicativo cliente não deve exibir nem executar a ação, a não ser que o aplicativo tenha um conhecimento personalizado e não genérico da ação específica. As ações proprietárias não são retornadas para o aplicativo cliente, a menos que o aplicativo cliente solicite explicitamente essas definindo a restrição adequada no **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Tipos de invocação  
 A tabela a seguir descreve os diferentes tipos de invocação disponíveis no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O tipo de invocação é usado somente pelo aplicativo cliente para ajudar a determinar quando a ação deve ser invocada. O tipo de invocação não determina realmente o comportamento de invocação da ação.  
  
|Tipo de invocação|Description|  
|---------------------|-----------------|  
|**INTERATIVO**|A ação deve ser invocada pelo aplicativo cliente por meio da interação do usuário.|  
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
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

