---
title: Fazer upgrade do Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: "79"
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4286f2266d115d39ad97ff3f6255187e7a01d968
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="upgrade-analysis-services"></a>Atualizar o Analysis Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] As instâncias do Analysis Services podem ser atualizadas para uma versão do SQL Server do mesmo modo de servidor para aproveitar os recursos introduzidos na versão atual, conforme descrito em [Novidades do Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md).  
  
 Você pode fazer uma atualização in-loco de cada instância, mesmo se houver outras instâncias em execução no mesmo hardware. No entanto, a maioria dos administradores opta por instalar uma nova instância da nova versão para teste de aplicativos, antes de transferir cargas de trabalho de produção para o novo servidor. Mas, para servidores de desenvolvimento ou de teste, pode ser mais prático fazer uma atualização in-loco.  
  
## <a name="server-upgrade"></a>Upgrade do servidor  
 Há dois métodos básicos para atualização de servidores e bancos de dados:  
  
> [!NOTE]
> Os níveis de compatibilidade de bancos de dados associados a um determinado servidor permanecem iguais, a menos que você os altere manualmente.
   
  
### <a name="in-place-upgrade"></a>Atualização in-loco  
 O processo de upgrade migra automaticamente os bancos de dados existentes da instância antiga para a nova instância. Como os metadados e os dados binários são incompatíveis entre as duas versões, você reterá os dados depois de atualizar e não precisará migrar os dados manualmente.  
  
 Para atualizar uma instância existente, execute a Instalação e especifique o nome da instância existente como o nome da nova instância.  
  
### <a name="side-by-side-upgrade"></a>Atualização lado a lado  
  
-   Faça um backup de todos os bancos de dados e verifique se é possível restaurá-los. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
-   Identifique um subconjunto dos relatórios, planilhas ou instantâneos de painel a ser usado posteriormente, como base para a confirmação das operações do servidor após a atualização. Se possível, colete medições de desempenho para que você possa fazer comparações em relação às cargas de trabalho em um servidor atualizado.  
  
-   Instale uma nova instância do Analysis Services, escolhendo o mesmo modo de servidor (de tabela ou multidimensional), de acordo com o servidor que você pretende substituir. 
  
     Execute as tarefas pós-instalação para configurar portas e adicionar administradores de servidor. Para saber mais, consulte [Configuração pós-instalação &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md).  
  
-   Anexe ou restaure os bancos de dados.  
  
-   Execute o DBCC para verificar a integridade do banco de dados. Os modelos de tabela passam por uma verificação mais completa com testes para objetos órfãos, em toda a hierarquia do modelo. Para modelos multidimensionais, somente os índices da partição são verificados. Para saber mais, consulte [DBCC &#40;Verificador de Consistência de Banco de Dados&#41; para bancos de dados de tabela e multidimensionais do Analysis Services](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).  
  
-   Faça testes em relatórios, planilhas e painéis para confirmar que não há alterações prejudiciais de comportamento ou de cálculos. Você terá um desempenho mais rápido para as cargas de trabalho multidimensionais e de tabela.  
  
-   Teste as operações de processamento para corrigir problemas de logon ou de permissão. Se estiver usando uma conta de serviço padrão para conexões, o novo serviço será executado em uma conta diferente. Para saber mais, consulte [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
-   Teste as operações de backup e restauração no servidor atualizado, ajustando os scripts para usar o novo nome do servidor.  
  
## <a name="database-upgrade"></a>Atualização do banco de dados  
 Os bancos de dados que foram criados em versões anteriores são executados no servidor atualizado com a configuração do nível de compatibilidade original. De modo geral, você pode atualizar um banco de dados ou modelo para operar em um nível superior de compatibilidade para obter acesso a novos recursos. Mas, lembre-se de que, ao fazê-lo, estará associado a uma versão específica do servidor.  
  
 Para atualizar um banco de dados, normalmente você atualiza o modelo no SSDT (SQL Server Data Tools) e implanta a solução em uma instância do servidor atualizado.
  
 Os bancos de dados multidimensionais e de tabela seguem caminhos de versão diferentes. Coincidentemente, os modelos multidimensionais e de tabela têm níveis de compatibilidade numerados semelhantes.  Os modos se desenvolverão em diferentes proporções, caso as alterações do recurso afetem apenas um deles.  
  
 Para fins de conhecimento, a tabela a seguir resume os níveis de compatibilidade, mas não deixe de analisar os tópicos detalhadamente para entender o que cada nível fornece.  
  
||||  
|-|-|-|  
|Tabular|1400|SQL Server 2017|
|Tabular|1200|SQL Server 2016|  
|Tabular|1103|SQL Server 2014|  
|Tabular|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 e posterior|  
|Multidimensional|1050|SQL Server 2005, 2008, 2008 R2|  
  
 Para saber mais, consulte [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) e [Nível de compatibilidade de modelos de tabela do Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também  
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Atualizar Power Pivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
  
