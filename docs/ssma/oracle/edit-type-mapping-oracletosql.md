---
title: Editar mapeamento de tipo (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e4f90a6658f18d4cee35f33e118b309b0d99da6f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="edit-type-mapping-oracletosql"></a>Editar mapeamento de tipo (OracleToSQL)
O **editar mapeamento de tipo** caixa de diálogo permite que você especifique como os tipos são mapeados entre os objetos de banco de dados de origem e de destino.  
  
Você pode acessar essa caixa de diálogo em vários locais:  
  
-   Quando você seleciona um banco de dados de origem ou o objeto de banco de dados, o **mapeamento de tipo** guia é exibida à direita do Gerenciador de metadados. Clique em **adicionar** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
-   Sobre o **ferramentas** menu, selecione **configurações de projeto** ou **configurações de projeto padrão**. Na caixa de diálogo, selecione **mapeamento de tipo**. Clique em **adicionar** para adicionar um novo mapeamento de tipo, ou clique em **editar** para alterar um mapeamento de tipo existente.  
  
Mapeamentos de tipo de tabela específico de substituem o banco de dados e mapeamentos de tipo de projeto. Mapeamentos de banco de dados específico substituem mapeamentos de projeto.  
  
## <a name="options"></a>Opções  
**Tipo de fonte**  
Selecione o tipo de dados de origem para mapear para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
Se o tipo de dados é de comprimento variável, os campos a seguir serão exibido em **tipo de fonte de**:  
  
**De**  
Especifique o comprimento mínimo para que esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 10 para especificar que esse mapeamento é para um intervalo começando em **nchar(10)**.  
  
**Para**  
Especifique o comprimento máximo para que esse mapeamento. Por exemplo, para o **nchar** tipo de dados, você pode inserir 20 para especificar que esse mapeamento é para um intervalo terminando às **nchar(20)**.  
  
**Tipo de destino**  
Selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados ao qual o tipo de fonte de dados é mapeado. Quando o SSMA cria a tabela ou procedimento armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o tipo de fonte de dados será alterado para esse tipo de dados.  
  
Se o tipo de dados é de comprimento variável, o campo a seguir será exibido em **tipo de destino**:  
  
**Replace with**  
Especifique o tamanho de destino para que esse mapeamento. Por exemplo, para o **nvarchar** tipo de dados, você pode inserir 20 para especificar que o tipo de dados de origem especificado deve ser mapeado para **nvarchar (20)**.  
  

