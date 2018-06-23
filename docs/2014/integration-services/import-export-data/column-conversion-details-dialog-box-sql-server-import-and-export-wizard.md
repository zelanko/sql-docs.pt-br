---
title: Caixa de diálogo Detalhes da Conversão de Coluna (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cd97a1bb27858b9107312f3ac32ea61ce07f415b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013140"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Caixa de diálogo Detalhes da Conversão de Coluna (Assistente de Importação e Exportação do SQL Server)
  Use o **detalhes da conversão de coluna** caixa de diálogo para revisar informações detalhadas de conversão sobre uma coluna individual. Essas informações de conversão contêm o tipo de dados da coluna na origem e no destino, além da conversão a ser realizada pelo assistente. Essa página também relaciona os arquivos de mapeamento de tipo de dados usados pelo assistente para determinar as conversões de tipo de dados necessárias. O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala esses tipos de dados com o mapeamento de arquivos durante a instalação.  
  
 **Para abrir a caixa de diálogo Detalhes da conversão de coluna**  
  
1.  No **revisar problemas de tipo de dados** página do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard no **tabela** , selecione uma tabela.  
  
2.  No **mapeamento de tipo de dados** lista, clique duas vezes na linha que contém a coluna para a qual você deseja exibir detalhes da conversão.  
  
 Para saber mais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 A finalidade de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação é copiar dados de uma fonte para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
  