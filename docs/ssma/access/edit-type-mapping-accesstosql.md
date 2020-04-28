---
title: Editar mapeamento de tipo (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7d41fc2f01e2cfbc2b20c58ea9be640f2afd8ea0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006577"
---
# <a name="edit-type-mapping-accesstosql"></a>Editar mapeamento de tipo (AccessToSQL)
A caixa de diálogo **Editar mapeamento de tipo** permite especificar como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou objeto de banco de dados, a guia **mapeamento de tipo** é exibida à direita do Gerenciador de metadados. Clique em **Adicionar** para adicionar um novo mapeamento de tipo ou clique em **Editar** para alterar um mapeamento de tipo existente.  
  
-   No menu **ferramentas** , selecione **configurações do projeto** ou **configurações padrão do projeto**. Na caixa de diálogo resultante, selecione **mapeamento de tipo**. Clique em **Adicionar** para adicionar um novo mapeamento de tipo ou clique em **Editar** para alterar um mapeamento de tipo existente.  
  
Os mapeamentos de tipo específicos de tabela substituem o banco de dados e os mapeamentos de tipo de projeto. Mapeamentos específicos de banco de dados substituem mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
**Tipo de fonte**  
Selecione o tipo de dados de origem para mapear para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
Se o tipo de dados for de comprimento variável, os campos a seguir aparecerão em **tipo de origem**:  
  
**De**  
Especifique o comprimento mínimo para esse mapeamento. Por exemplo, para o tipo de dados **texto** , você pode inserir 10 para especificar que esse mapeamento é para um intervalo que começa no **texto (10)**.  
  
**Para**  
Especifique o comprimento máximo para esse mapeamento. Por exemplo, para o tipo de dados **texto** , você pode inserir 20 para especificar que esse mapeamento é para um intervalo que termina no **texto (20)**.  
  
**Tipo de destino**  
Selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados para o qual o tipo de dados de origem está mapeado. Quando o SSMA cria a tabela ou o procedimento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]armazenado no, o tipo de dados de origem será alterado para esse tipo de dados.  
  
Se o tipo de dados for de comprimento variável, o campo a seguir aparecerá em **tipo de destino**:  
  
**Replace with**  
Especifique o comprimento de destino para esse mapeamento. Por exemplo, para o tipo de dados **nvarchar** , você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20)**.  
  
