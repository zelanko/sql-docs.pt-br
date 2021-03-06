---
description: Configurações do projeto (mapeamento de tipo) (AccessToSQL)
title: Configurações do projeto (mapeamento de tipo) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8c39bc03cb6a1da09c7be6aac41c18b9d3bbd871
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987522"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Configurações do projeto (mapeamento de tipo) (AccessToSQL)
As configurações do projeto de mapeamento de tipo permitem que você defina mapeamentos de tipo padrão para o projeto do SSMA. Você também pode especificar mapeamentos de tipo para objetos de banco de dados individuais. Para obter mais informações, consulte [mapeando tipos de dados de origem e de destino](mapping-source-and-target-data-types-accesstosql.md).  
  
O mapeamento de tipo está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :  
  
-   Use a caixa de diálogo **configurações do projeto** para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo, no menu **ferramentas** , selecione **configurações do projeto**e, em seguida, clique em mapeamento de **tipo** no painel esquerdo.  
  
-   Use a caixa de diálogo **configurações de projeto padrão** para definir opções de configuração para todos os projetos. Para acessar as configurações de mapeamento de tipo, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas/Changed do menu suspenso **versão de destino de migração** e clique em mapeamento de **tipo** no painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados do Access a ser mapeado.  
  
**Tipo de destino**  
O tipo de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure para o tipo de dados de acesso especificado.  
  
A tabela a seguir mostra o mapeamento padrão entre os tipos de dados de origem e de destino.  
  
|Acessar tipo de dados|Tipo de dados do SQL Server|  
|--------------------|------------------------|  
|**binário [ \* .. \* ]**|**varbinary [ \* ]**|  
|**booleano**|**bit**|  
|**byte**|**tinyint**|  
|**moeda**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**duplo**|**flutuante**|  
|**guid**|**uniqueidentifier**|  
|**inteiro**|**smallint**|  
|**longo**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**campos**|**nvarchar(max)**|  
|**memorando** -para o Access 97|**varchar(max)**|  
|**single**|**real**|  
|**texto [ \* .. \* ]**|**nvarchar [ \* ]**|  
|**text [ \* .. \* ]** -para o Access 97|**varchar [ \* ]**|  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar um tipo de dados na lista mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Restaurar Padrões**  
Clique para redefinir todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
## <a name="see-also"></a>Consulte Também  
[Mapeamento de tipo de dados de destino e de origem](mapping-source-and-target-data-types-accesstosql.md)  
[Referência da interface do usuário (Access)](./user-interface-reference-accesstosql.md)  
