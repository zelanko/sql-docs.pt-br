---
title: Chamando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55569f23ae943e96a495905434bb0d39f2796a63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727752"
---
# <a name="calling-stored-procedures"></a>Chamando procedimentos armazenados
  Procedimentos armazenados podem ser chamados no servidor ou a partir de um aplicativo cliente. Nos dois casos, os procedimentos armazenados são sempre executados no servidor, no contexto do servidor ou de um banco de dados. Não há permissões especiais necessárias para executar um procedimento armazenado. Uma vez adicionado o procedimento armazenado por um assembly ao contexto do servidor ou do banco de dados, qualquer usuário pode executá-lo desde que a função do usuário permita as ações realizadas pelo procedimento armazenado.  
  
 O procedimento armazenado em formato MDX é chamado da mesma forma que se chama uma função MDX intrínseca. No caso de um procedimento armazenado sem-parâmetros, o nome do procedimento e um par de parênteses vazios são usados, como mostrado a seguir:  
  
```  
MyStoredProcedure()  
```  
  
 Se o procedimento armazenado tiver um ou mais parâmetros, eles são fornecidos, em ordem, separados por vírgulas. Este é um exemplo de procedimento armazenado com três parâmetros:  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>Chamando procedimentos armazenados em consultas MDX  
 Em todas as consultas MDX, o procedimento armazenado deve retornar o tipo sintaticamente correto exigido por uma expressão MDX. Se um procedimento armazenado não retornar o tipo correto, ocorrerá um erro da linguagem MDX. Os exemplos a seguir demonstram procedimentos armazenados que retornam um conjunto, um membro e o resultado de uma operação matemática.  
  
### <a name="returning-a-set"></a>Retornando um conjunto  
 Os exemplos a seguir implementam um procedimento armazenado, chamado MySproc, que retorna um conjunto. No primeiro exemplo, MySproc retorna o conjunto diretamente na expressão SELECT. Nos dois segundos exemplos, MySproc retorna o conjunto como um argumento para as funções Crossjoin e DrilldownLevel.  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>Retornando um membro  
 O exemplo a seguir mostra uma função MySproc que retorna um membro:  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>Retornando o resultado de uma operação matemática  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>Chamando procedimentos armazenados com a instrução Call  
 É possível chamar procedimentos armazenados fora do contexto de uma consulta MDX usando a instrução MDX `Call`.  
  
 Use esse método para instanciar os efeitos colaterais de uma consulta armazenada ou para o aplicativo obter os resultados de uma consulta armazenada. Um uso comum da instrução `Call` seria para usar o Analysis Management Objects (AMO) para executar funções administrativas que não têm um resultado retornado. Por exemplo, o comando a seguir chama um procedimento armazenado:  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 O único tipo com suporte retornado a partir de um procedimento armazenado em uma instrução `Call` é um conjunto de linhas. A serialização de um conjunto de linhas é definido pelo XML for Analysis. Se um procedimento armazenado em uma instrução `Call` retornar qualquer outro tipo, ele será ignorado e não será retornado em XML para o aplicativo que o chamou. Para obter mais informações sobre conjuntos de linhas do XML for Analysis, consulte Conjuntos de linhas de esquema do XML for Analysis.  
  
 Se o procedimento armazenado retornar um conjunto de linhas do .NET, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converterá o resultado no servidor em um conjunto de linhas do XML for Analysis. O conjunto de linhas do XML for Analysis é sempre retornado por um procedimento armazenado na função `Call`. Se um conjunto de dados contiver recursos que não possam ser expressos no conjunto de linhas do XML for Analysis, ocorrerá uma falha.  
  
 Também podem ser empregados procedimentos que retornam valores nulos (por exemplo, sub-rotinas em Visual Basic) com a palavra-chave CALL. Se, por exemplo, você quiser usar a função MyVoidFunction() em uma instrução MDX, a seguinte sintaxe será empregada:  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
