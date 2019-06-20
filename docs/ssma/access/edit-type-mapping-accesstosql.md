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
manager: craigg
ms.openlocfilehash: 2bbe1636db483ad24f7744fe4d9902c520e07dbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138858"
---
# <a name="edit-type-mapping-accesstosql"></a>Editar mapeamento de tipo (AccessToSQL)
O **editar mapeamento de tipo** caixa de diálogo permite que você especifique como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou o objeto de banco de dados, o **mapeamento de tipo** guia é exibida à direita do Gerenciador de metadados. Clique em **Add** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Sobre o **ferramentas** menu, selecione **configurações do projeto** ou **configurações de projeto padrão**. Na caixa de diálogo resultante, selecione **mapeamento de tipo**. Clique em **Add** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
Mapeamentos de tipo de tabela específicas de substituem o banco de dados e mapeamentos de tipo de projeto. Mapeamentos de banco de dados específicos substituem os mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
**Tipo de fonte**  
Selecione o tipo de dados de origem para mapear para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
Se for o tipo de dados de comprimento variável, os campos a seguir aparecerá sob **tipo de fonte**:  
  
**De**  
Especifique o comprimento mínimo para esse mapeamento. Por exemplo, para o **texto** tipo de dados, você pode inserir 10 para especificar que esse mapeamento é para um intervalo começando **text(10)** .  
  
**Para**  
Especifique o comprimento máximo para esse mapeamento. Por exemplo, para o **texto** tipo de dados, você pode inserir 20 para especificar que esse mapeamento é para um intervalo terminando às **text(20)** .  
  
**Tipo de destino**  
Selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados ao qual o tipo de fonte de dados é mapeado. Quando o SSMA cria a tabela ou procedimento armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o tipo de fonte de dados será alterado para esse tipo de dados.  
  
Se for o tipo de dados de comprimento variável, o campo a seguir aparecerá sob **tipo de destino**:  
  
**Replace with**  
Especifique o comprimento de destino para esse mapeamento. Por exemplo, para o **nvarchar** tipo de dados, você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20)** .  
  
