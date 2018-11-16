---
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8a695217909641c737b7780fc4f8b80b2cb08152
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681244"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Configurações do projeto (mapeamento de tipo) (AccessToSQL)
As configurações de mapeamento de tipo de projeto permitem que você definir mapeamentos de tipo padrão para o projeto do SSMA. Você também pode especificar mapeamentos de tipo para objetos de banco de dados individuais. Para obter mais informações, consulte [tipos de dados de destino e origem do mapeamento](mapping-source-and-target-data-types-accesstosql.md).  
  
Mapeamento de tipo está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo:  
  
-   Use o **configurações do projeto** caixa de diálogo para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo na **ferramentas** menu, selecione **configurações do projeto**e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de mapeamento de tipo na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida / alterado de  **Versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** no painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados do Access para mapear.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipo de dados do SQL Azure para o tipo de dados de acesso especificado.  
  
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
  
**Restaurar Padrões**  
Clique para redefinir todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de tipo de dados de destino e de origem](mapping-source-and-target-data-types-accesstosql.md)  
[Reference(Access) de Interface do usuário](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
