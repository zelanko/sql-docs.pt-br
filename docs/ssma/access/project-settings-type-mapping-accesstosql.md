---
title: Configurações (mapeamento de tipo) do projeto (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bd5bc6a0db71d2836c068a261681d813bc2011b3
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774462"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Configurações (mapeamento de tipo) do projeto (AccessToSQL)
As configurações de mapeamento de tipo de projeto permitem definir mapeamentos de tipo de padrão para o projeto SSMA. Você também pode especificar mapeamentos de tipo para objetos de banco de dados individuais. Para obter mais informações, consulte [tipos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
Mapeamento de tipo está disponível no **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo:  
  
-   Use o **configurações de projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo, no **ferramentas** menu, selecione **configurações de projeto**e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de mapeamento de tipo, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido e alterado de **versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados do Access para mapear.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipo de dados do SQL Azure para o tipo de dados de acesso especificado.  
  
A tabela a seguir mostra o mapeamento padrão entre tipos de dados de origem e destino.  
  
|Tipo de dados do Access|Tipo de dados do SQL Server|  
|--------------------|------------------------|  
|**binário [\*... \*]**|**varbinary[\*]**|  
|**booleano**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**inteiro**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**Memorando** - para Access 97|**varchar(max)**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**texto [\*... \*]** - para o Access 97|**varchar[\*]**|  
  
**Adicionar**  
Clique para adicionar um tipo de dados para a lista de mapeamento.  
  
**Editar**  
Clique para editar um tipo de dados na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Redefinir para padrão**  
Clique para restaurar todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de tipo de dados de destino e de origem](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
