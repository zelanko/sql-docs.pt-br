---
title: Editar mapeamento de tipo (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8db4278a82968a5bd147f5fcb984af3fa104022e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="edit-type-mapping-mysqltosql"></a>Editar mapeamento de tipo (MySQLToSQL)
O **editar mapeamento de tipo** caixa de diálogo permite que você especifique como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou o objeto de banco de dados, o **mapeamento de tipo** guia é exibida à direita do Gerenciador de metadados. Clique em **adicionar** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Sobre o **ferramentas** menu, selecione **configurações de projeto** ou **configurações de projeto padrão**. Na caixa de diálogo, selecione **mapeamento de tipo**. Clique em **adicionar** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Mapeamentos de tipo de tabela específico de substituem o banco de dados e mapeamentos de tipo de projeto. Mapeamentos de banco de dados específico substituem mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
  
##### <a name="source-type"></a>Tipo de fonte  
Selecione o tipo de dados de origem para mapear para um tipo de dados do SQL Server.  
  
Se o tipo de dados é de comprimento variável, os campos a seguir serão exibido em **Sourcetype**:  
  
##### <a name="from"></a>De  
Especifique o comprimento mínimo para que esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 10 para especificar que esse mapeamento é para um intervalo começando em **nchar(10).**  
  
##### <a name="to"></a>Para  
Especifique o comprimento máximo para que esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 20 para especificar que esse mapeamento é para um intervalo de término em **nchar(20).**  
  
##### <a name="target-type"></a>Tipo de destino  
Selecione o tipo de dados do SQL Server ao qual o tipo de fonte de dados é mapeado. Quando o SSMA cria a tabela ou no SQL Server, o tipo de fonte de dados será alterado para esse tipo de dados.  
  
Se o tipo de dados é de comprimento variável, o campo a seguir será exibido em **tipo de destino**:  
  
##### <a name="replace-with"></a>Substitua por  
Especifique o tamanho de destino para que esse mapeamento. Por exemplo, para o **nvarchar** tipo de dados, você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20).**  
  
