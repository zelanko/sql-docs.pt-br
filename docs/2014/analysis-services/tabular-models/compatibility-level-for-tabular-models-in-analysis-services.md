---
title: Nível de compatibilidade (SSAS Tabular SP1) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 74aad4a5d8b6f387845f2134b236a15bb75d4689
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006204"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>Nível de compatibilidade (SP1 de tabela SSAS)
  Você pode especificar *nível de compatibilidade* ao criar novos projetos de modelo de tabela, ao atualizar projetos existentes de modelo de tabela, ao atualizar implantados existentes bancos de dados de modelo de tabela, ou ao importar pastas de trabalho PowerPivot.  
  
## <a name="compatibility-level"></a>Nível de Compatibilidade  
 É comum instalar novas versões e service packs em computadores de desenvolvimento e teste antes de instalá-los em computadores de produção. Nesses casos, é importante entender o nível de compatibilidade de configuração dos novos projetos de modelo de tabela e daqueles já implantados em um ambiente de produção.  
  
 Uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services oferece suporte aos seguintes níveis de compatibilidade (versão do banco de dados):  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>Definir o nível de compatibilidade ao criar um novo projeto de modelo de tabela  
 Ao criar um novo projeto de modelo de tabela no SSDT SQL Server Data Tools (), no **nova tabela opções de projeto** caixa de diálogo que você pode especificar o nível de compatibilidade. É possível escolher entre criar um novo projeto a ser implantado em uma instância do [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior do Analysis Services ou em uma instância do SQL Server 2012 Analysis Services (sem o Service Pack 1).  
  
 Você também pode especificar um nível de compatibilidade padrão selecionando a opção **Não mostrar esta mensagem novamente** . Todos os projetos subsequentes usarão o nível de compatibilidade especificado. É possível alterar o nível de compatibilidade padrão no SSDT em Opções.  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>Atualizar um projeto de modelo de tabela existente para o nível de compatibilidade 1103  
 Você pode atualizar um projeto de modelo de tabela criado no SSDT antes de instalar [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior para a versão 1103 do banco de dados compatível com o uso de **nível de compatibilidade** propriedade no modelo **propriedades**janela. Para atualizar um projeto de modelo de tabela, o computador em que o SSDT está instalado deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior instalado e a instância do Analysis Services na qual o banco de dados de espaço de trabalho reside também deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] instalado. Não é possível fazer downgrade para uma versão anterior.  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>Atualizar um banco de dados modelo de tabela implantado para o nível de compatibilidade 1103  
 Você pode atualizar uma versão de banco de dados no banco de dados de modelo de tabela implantado existente 1103 compatível no SQL Server Management Studio (SSMS) usando o **nível de compatibilidade** propriedade **propriedades de banco de dados**. Para atualizar, o computador no qual a instância do SQL Server Analysis Services está instalada deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior instalado. Não é possível fazer downgrade de um banco de dados modelo de tabela implantado para uma versão anterior.  
  
### <a name="import-from-powerpivot"></a>Importar do PowerPivot  
 Ao criar um novo projeto de modelo de tabela importando do PowerPivot, você pode especificar se deseja atualizar o nível de compatibilidade para o nível de compatibilidade padrão (se configurado previamente no SSDT) ou deixar o nível de compatibilidade já especificado na pasta de trabalho PowerPivot.  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>Verificar o nível de compatibilidade de um banco de dados modelo de tabela no SSMS  
 Você pode verificar o nível de compatibilidade para um banco de dados de modelo de tabela no SSMS exibindo a **nível de compatibilidade** propriedade (novo no [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) em **propriedades de banco de dados**.  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>Verificar o nível de compatibilidade com suporte para uma instância do Analysis Services no SSMS  
 Você pode verificar o nível de compatibilidade com suporte no SSMS exibindo a **nível de compatibilidade com suporte** propriedade o **informações** página (novo no [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) em **análise Propriedades de serviços**. Um nível de compatibilidade de 1103 com suporte indica que o SQL Server SP1 ou posterior está instalado. O nível de compatibilidade com suporte não pode ser alterado.  
  
  