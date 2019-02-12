---
title: A consulta de design | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4ce60e8326149ac0d8e7f54a84dd344f5088ee3d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032614"
---
# <a name="design-the-query"></a>Projetar a consulta
  Use esta página do Assistente de Relatório para criar uma consulta, digitando a consulta manualmente, usando o Construtor de Consultas para criar uma consulta interativamente ou importando uma consulta de outro relatório.  
  
 O tipo de fonte de dados que você escolheu na página Selecionar a Fonte de Dados, uma página anterior do Assistente de Relatório, determina a consulta que você pode digitar nessa página. Por exemplo, se o tipo de fonte de dados for [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você poderá digitar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] ou nomes de procedimento armazenado. Se o tipo de fonte de dados for [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o painel Consulta será desabilitado e você não poderá digitar uma consulta diretamente. Você pode especificar a consulta usando o Construtor de Consultas.  
  
## <a name="options"></a>Opções  
 **Cadeia de caracteres de consulta**  
 Digite uma consulta que recupere os dados que você deseja usar em seu relatório.  
  
 **Construtor de Consultas**  
 Clique em **Construtor de Consultas** para abrir um designer de consulta para a fonte de dados ou importar uma consulta de outro relatório.  
  
 Para obter mais informações sobre designers de consulta, consulte [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md).  
  
## <a name="example"></a>Exemplo  
 Para o tipo de fonte de dados **Microsoft SQL Server**, a consulta a seguir recupera uma lista de sobrenomes das [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados `Person` tabela.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Para o tipo de fonte de dados **Microsoft SQL Server**, a seguinte consulta executa o [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] procedimento armazenado `uspGetEmployeeManagers` para o funcionário com identificação número 1:  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Assistente de relatório](../../2014/reporting-services/report-wizard-help.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
