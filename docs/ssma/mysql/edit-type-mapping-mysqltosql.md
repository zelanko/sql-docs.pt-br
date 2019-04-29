---
title: Editar mapeamento de tipo (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 98b7c0433e506d7ef6e825199a9a6629c52e6f3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183086"
---
# <a name="edit-type-mapping-mysqltosql"></a>Editar mapeamento de tipo (MySQLToSQL)
O **editar mapeamento de tipo** caixa de diálogo permite que você especifique como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou o objeto de banco de dados, o **mapeamento de tipo** guia é exibida à direita do Gerenciador de metadados. Clique em **Add** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Sobre o **ferramentas** menu, selecione **configurações do projeto** ou **configurações de projeto padrão**. Na caixa de diálogo resultante, selecione **mapeamento de tipo**. Clique em **Add** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Mapeamentos de tipo de tabela específicas de substituem o banco de dados e mapeamentos de tipo de projeto. Mapeamentos de banco de dados específicos substituem os mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
  
##### <a name="source-type"></a>Tipo de fonte  
Selecione o tipo de dados de origem para mapear para um tipo de dados do SQL Server.  
  
Se for o tipo de dados de comprimento variável, os campos a seguir aparecerá sob **Sourcetype**:  
  
##### <a name="from"></a>De  
Especifique o comprimento mínimo para esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 10 para especificar que esse mapeamento é para um intervalo começando em **nchar(10).**  
  
##### <a name="to"></a>Para  
Especifique o comprimento máximo para esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 20 para especificar que esse mapeamento é para um intervalo terminando às **nchar(20).**  
  
##### <a name="target-type"></a>Tipo de destino  
Selecione o tipo de dados do SQL Server ao qual o tipo de fonte de dados é mapeado. Quando o SSMA cria a tabela ou no SQL Server, o tipo de fonte de dados será alterado para esse tipo de dados.  
  
Se for o tipo de dados de comprimento variável, o campo a seguir aparecerá sob **tipo de destino**:  
  
##### <a name="replace-with"></a>Substitua por  
Especifique o comprimento de destino para esse mapeamento. Por exemplo, para o **nvarchar** tipo de dados, você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20).**  
  
