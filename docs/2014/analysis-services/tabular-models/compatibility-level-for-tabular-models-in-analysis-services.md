---
title: Nível de compatibilidade (SSAS tabular SP1) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57a1e67db8bcbf17dc964f7341df25a396c36ad0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067595"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>Nível de compatibilidade (SP1 de tabela SSAS)
  Você pode especificar o *nível de compatibilidade* ao criar novos projetos de modelo de tabela ao atualizar projetos de modelo de tabela existentes, ao atualizar os bancos de dados de modelo de tabela implantados existentes ou ao importar pastas de trabalho PowerPivot.  
  
## <a name="compatibility-level"></a>Nível de Compatibilidade  
 É comum instalar novas versões e service packs em computadores de desenvolvimento e teste antes de instalá-los em computadores de produção. Nesses casos, é importante entender o nível de compatibilidade de configuração dos novos projetos de modelo de tabela e daqueles já implantados em um ambiente de produção.  
  
 Uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services oferece suporte aos seguintes níveis de compatibilidade (versão do banco de dados):  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>Definir o nível de compatibilidade ao criar um novo projeto de modelo de tabela  
 Ao criar um novo projeto de modelo de tabela no SQL Server Data Tools (SSDT), na caixa de diálogo **novas opções de projeto de tabela** , você pode especificar o nível de compatibilidade. É possível escolher entre criar um novo projeto a ser implantado em uma instância do [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior do Analysis Services ou em uma instância do SQL Server 2012 Analysis Services (sem o Service Pack 1).  
  
 Você também pode especificar um nível de compatibilidade padrão selecionando a opção **Não mostrar esta mensagem novamente** . Todos os projetos subsequentes usarão o nível de compatibilidade especificado. É possível alterar o nível de compatibilidade padrão no SSDT em Opções.  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>Atualizar um projeto de modelo de tabela existente para o nível de compatibilidade 1103  
 Você pode atualizar um projeto de modelo de tabela criado no SSDT antes [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] de instalar ou posterior para ser compatível com a versão 1103 do banco de dados usando a propriedade **nível de compatibilidade** na janela **Propriedades** do modelo. Para atualizar um projeto de modelo de tabela, o computador em que o SSDT está instalado deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior instalado e a instância do Analysis Services na qual o banco de dados de workspace reside também deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] instalado. Não é possível fazer downgrade para uma versão anterior.  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>Atualizar um banco de dados modelo de tabela implantado para o nível de compatibilidade 1103  
 Você pode atualizar um banco de dados modelo de tabela implantado existente para o banco de dados versão 1103 compatível com o SSMS (SQL Server Management Studio) usando a propriedade **nível de compatibilidade** nas propriedades do **banco de dados**. Para atualizar, o computador no qual a instância do SQL Server Analysis Services está instalada deve ter o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior instalado. Não é possível fazer downgrade de um banco de dados modelo de tabela implantado para uma versão anterior.  
  
### <a name="import-from-powerpivot"></a>Importar do PowerPivot  
 Ao criar um novo projeto de modelo de tabela importando do PowerPivot, você pode especificar se deseja atualizar o nível de compatibilidade para o nível de compatibilidade padrão (se configurado previamente no SSDT) ou deixar o nível de compatibilidade já especificado na pasta de trabalho PowerPivot.  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>Verificar o nível de compatibilidade de um banco de dados modelo de tabela no SSMS  
 Você pode verificar o nível de compatibilidade de um banco de dados modelo de tabela no SSMS exibindo a propriedade nível [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]de **compatibilidade** (novo no) nas propriedades do banco de **dados**.  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>Verificar o nível de compatibilidade com suporte para uma instância do Analysis Services no SSMS  
 Você pode verificar o nível de compatibilidade com suporte no SSMS exibindo a propriedade **nível de compatibilidade com suporte** na página **informações** (novo no [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) em Propriedades de **Analysis Services**. Um nível de compatibilidade de 1103 com suporte indica que o SQL Server SP1 ou posterior está instalado. O nível de compatibilidade com suporte não pode ser alterado.  
  
  
