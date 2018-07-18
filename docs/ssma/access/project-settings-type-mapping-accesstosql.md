---
title: Configurações do projeto (mapeamento de tipo) (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 0403c7074df0f81081cda167fe9bbf04626f2522
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985738"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Configurações do projeto (mapeamento de tipo) (AccessToSQL)
As configurações de mapeamento de tipo de projeto permitem que você definir mapeamentos de tipo padrão para o projeto do SSMA. Você também pode especificar mapeamentos de tipo para objetos de banco de dados individuais. Para obter mais informações, consulte [tipos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
Mapeamento de tipo está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo:  
  
-   Use o **configurações do projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo na **ferramentas** menu, selecione **configurações do projeto**e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de mapeamento de tipo na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida / alterado de  **Versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados do Access para mapear.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipo de dados do SQL Azure para o tipo de dados de acesso especificado.  
  
A tabela a seguir mostra o mapeamento padrão entre os tipos de dados de origem e destino.  
  
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
|**texto [\*... \*]** - para Access 97|**varchar[\*]**|  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar um tipo de dados na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Redefinir para padrão**  
Clique para redefinir todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de tipo de dados de destino e de origem](http://msdn.microsoft.com/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
