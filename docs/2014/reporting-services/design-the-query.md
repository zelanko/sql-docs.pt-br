---
title: Criar a consulta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f09964013bdc8675e5d4701bd86421317c33fc97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109291"
---
# <a name="design-the-query"></a>Projetar a consulta
  Use esta página do Assistente de Relatório para criar uma consulta, digitando a consulta manualmente, usando o Construtor de Consultas para criar uma consulta interativamente ou importando uma consulta de outro relatório.  
  
 O tipo de fonte de dados que você escolheu na página Selecionar a Fonte de Dados, uma página anterior do Assistente de Relatório, determina a consulta que você pode digitar nessa página. Por exemplo, se o tipo de fonte de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]dados for, você [!INCLUDE[tsql](../includes/tsql-md.md)] poderá inserir instruções ou nomes de procedimento armazenado. Se o tipo de fonte de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]dados for, o painel de consulta será desabilitado e você não poderá inserir uma consulta diretamente. Você pode especificar a consulta usando o Construtor de Consultas.  
  
## <a name="options"></a>Opções  
 **Cadeia de consulta**  
 Digite uma consulta que recupere os dados que você deseja usar em seu relatório.  
  
 **Construtor de Consultas**  
 Clique em **Construtor de Consultas** para abrir um designer de consulta para a fonte de dados ou importar uma consulta de outro relatório.  
  
 Para obter mais informações sobre designers de consulta, consulte [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md).  
  
## <a name="example"></a>Exemplo  
 Para o tipo de fonte de dados **Microsoft SQL Server**, a consulta a seguir recupera uma lista de últimos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] nomes `Person` da tabela de banco de dado.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Para o tipo de fonte de dados **Microsoft SQL Server**, a consulta a [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] seguir executa `uspGetEmployeeManagers` o procedimento armazenado para o funcionário com identificação número 1:  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda do assistente de relatório](../../2014/reporting-services/report-wizard-help.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
