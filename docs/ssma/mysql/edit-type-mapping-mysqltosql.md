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
ms.openlocfilehash: d31304dae7246e425ef54af6d1382af7e885696c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103005"
---
# <a name="edit-type-mapping-mysqltosql"></a>Editar mapeamento de tipo (MySQLToSQL)
A caixa de diálogo **Editar mapeamento de tipo** permite especificar como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou objeto de banco de dados, a guia **mapeamento de tipo** é exibida à direita do Gerenciador de metadados. Clique em **Adicionar** para adicionar um novo mapeamento de tipo ou clique em **Editar** para alterar um mapeamento de tipo existente.  
  
-   No menu **ferramentas** , selecione **configurações do projeto** ou **configurações padrão do projeto**. Na caixa de diálogo resultante, selecione **mapeamento de tipo**. Clique em **Adicionar** para adicionar um novo mapeamento de tipo ou clique em **Editar** para alterar um mapeamento de tipo existente.  
  
-   Os mapeamentos de tipo específicos de tabela substituem o banco de dados e os mapeamentos de tipo de projeto. Mapeamentos específicos de banco de dados substituem mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
  
##### <a name="source-type"></a>Tipo de origem  
Selecione o tipo de dados de origem para mapear para um tipo de dados SQL Server.  
  
Se o tipo de dados for de comprimento variável, os seguintes campos aparecerão sob **SourceType**:  
  
##### <a name="from"></a>De  
Especifique o comprimento mínimo para esse mapeamento. Por exemplo, para o tipo de dados **nchar** , você pode inserir 10 para especificar que esse mapeamento é para um intervalo que começa em **nchar (10).**  
  
##### <a name="to"></a>Para  
Especifique o comprimento máximo para esse mapeamento. Por exemplo, para o tipo de dados **nchar** , você pode inserir 20 para especificar que esse mapeamento é para um intervalo que termina em **nchar (20).**  
  
##### <a name="target-type"></a>Tipo de destino  
Selecione o tipo de dados SQL Server para o qual o tipo de dados de origem está mapeado. Quando o SSMA cria a tabela ou na SQL Server, o tipo de dados de origem será alterado para esse tipo de dados.  
  
Se o tipo de dados for de comprimento variável, o campo a seguir aparecerá em **tipo de destino**:  
  
##### <a name="replace-with"></a>Substitua por  
Especifique o comprimento de destino para esse mapeamento. Por exemplo, para o tipo de dados **nvarchar** , você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20).**  
  
