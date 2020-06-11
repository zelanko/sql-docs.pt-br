---
title: Caixa de diálogo Criar consulta de processamento (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createprocessingquerydialog.f1
ms.assetid: c133d624-f35e-486e-be9f-ceafd906f168
author: minewiskan
ms.author: owend
ms.openlocfilehash: 185ea27c344ccb9e06f914507faca3fea9554dae
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526424"
---
# <a name="create-processing-query-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Criar Consulta de Processamento (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Criar Consulta de Processamento** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar uma consulta de processamento na guia **Notificações** da caixa de diálogo **Opções de Armazenamento** . Uma consulta de processamento é uma consulta que retorna um conjunto de linhas contendo as alterações feitas em uma tabela associada a um objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] desde a última sondagem na tabela, para atualização incremental do cache MOLAP (OLAP multidimensional) do objeto. O Analysis Services usa outra consulta, referenciada como uma consulta sondagem, para sondar uma tabela associada a um objeto e determinar se a tabela foi alterada. Consultas de processamento não são necessárias ao atualizar o cache MOLAP do objeto completamente.  
  
 Normalmente, a consulta de processamento é parametrizada, e dois parâmetros têm suporte no momento:  
  
-   O valor de singleton retornado pela consulta sondagem durante a sondagem agendada anterior.  
  
-   O valor de singleton retornado pela consulta sondagem durante a sondagem agendada atual.  
  
 Por exemplo, as consultas listadas na tabela a seguir podem ser usadas para atualização incremental da dimensão do Cliente no projeto de exemplo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] da Adventure Works DW.  
  
|Tipo de consulta|Instrução de consulta|  
|----------------|---------------------|  
|Consulta sondagem|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|Consulta de processamento|`SELECT`<br /><br /> `*`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`<br /><br /> `WHERE`<br /><br /> `(CustomerKey > COALESCE (@Param1, - 1))`<br /><br /> `AND (CustomerKey <= @Param2)`|  
  
 Para obter mais informações sobre atualizações incrementais para notificações de sondagens agendadas, consulte [Cache pró-ativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
 É possível exibir a caixa de diálogo **Criar Consulta de Processamento** clicando no botão de reticências ( **...** ) na coluna **Consulta de Processamento** da grade da opção **Sondagem agendada** na guia **Notificações** da caixa de diálogo **Opções de Armazenamento** . Para obter mais informações sobre a guia **Notificações** da caixa de diálogo **Opções de Armazenamento**, consulte [Notificações &#40;Caixa de diálogo Opções de Armazenamento&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).  
  
 A consulta digitada deve ser um comando de consulta válido para o provedor subjacente. A consulta é preparada com o provedor subjacente para validação e para identificar as colunas retornadas. A caixa de diálogo pode apresentar duas exibições:  
  
-   Construtor de Consultas VDT (Visual Database Tools)  
  
     Para todos os usuários, a exibição Construtor de Consultas VDT fornece um conjunto de ferramentas de interface do usuário para construir e testar uma consulta SQL visualmente.  
  
-   Construtor de Consultas Genérico  
  
     Para usuários avançados, a exibição Construtor de Consultas Genérico fornece uma interface do usuário mais simples e direta para construir e testar uma consulta SQL.  
  
## <a name="options"></a>Opções  
 **Fonte de Dados**  
 Especifica a fonte de dados para a consulta.  
  
 **Definição da consulta**  
 A definição da consulta fornece uma barra de ferramentas e painéis onde definir e testar a consulta, dependendo da exibição selecionada.  
  
 **Barra de ferramentas**  
 Use a barra de ferramentas para gerenciar conjuntos de dados, selecionar painéis para exibição e controlar várias funções de consulta.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Alternar para Construtor de Consultas Genérico**|Selecione para exibir apenas as opções disponíveis para a exibição Construtor de Consultas Genérico. Apenas as seguintes opções são exibidas:<br /><br /> **Painel SQL**<br /><br /> **Painel de resultados**<br /><br /> **Barra de Ferramentas**, contendo apenas **Alternar para o Construtor de Consultas VDT** e **Executar**<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Alternar para o Construtor de Consultas VDT**|Selecione para exibir todas as opções disponíveis para a exibição Construtor de Consultas VDT (Visual Database Tools).<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas Genérico** estiver selecionado.|  
|**Painel Mostrar/Ocultar Diagrama**|Mostra ou oculta o **painel de diagrama**.<br /><br /> **Observação** Essa opção só será exibida se **a opção Alternar para VDT Construtor de consultas** estiver selecionada.|  
|**Mostrar/Ocultar Painel Grade**|Mostra ou oculta o **painel de grade**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Painel Mostrar/Ocultar SQL**|Mostra ou oculta o painel **SQL**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Mostrar/Ocultar Painel Resultado**|Mostra ou oculta o painel **Resultado**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Executar**|Executa a consulta. Os resultados são exibidos no **painel de resultados**.|  
|**Verificar SQL**|Verifica a instrução SQL na consulta.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Classificação crescente**|Classifica as linhas de saída na coluna selecionada no painel **Grade**, em ordem crescente.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Classificação decrescente**|Classifica as linhas de saída na coluna selecionada no painel **Grade**, em ordem decrescente.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Remover filtro**|Remove critérios de classificação, se aplicável, para a linha selecionada no painel **Grade**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Usar Agrupar Por**|Adiciona a funcionalidade de agrupamento à consulta.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Adicionar Tabela**|Exibe a caixa de diálogo **Adicionar Tabela** para adicionar uma nova tabela ou exibição à consulta. Para obter mais informações sobre a caixa de diálogo **Adicionar Tabela**, consulte [Caixa de diálogo Adicionar Tabela &#40;Analysis Services – Dados Multidimensionais&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
  
 **Painel de diagrama**  
 Exibe os objetos referenciados pela consulta como um diagrama. O diagrama mostra as tabelas incluídas na consulta e como elas estão unidas. Marque ou desmarque a caixa de seleção próxima a uma coluna em uma tabela para adicioná-la ou removê-la da saída da consulta.  
  
 Quando você adiciona tabelas à consulta, a caixa de diálogo cria junções entre tabelas com base nas chaves da tabela. Para adicionar uma junção, arraste um campo de uma tabela sobre um campo em outra tabela. Para gerenciar uma junção, clique com o botão direito do mouse na junção.  
  
 Clique com o botão direito do mouse no **painel Diagrama** para adicionar ou remover tabelas, selecionar todas as tabelas e mostrar ou ocultar painéis.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
> [!IMPORTANT]  
>  A caixa de diálogo não oferece suporte para alteração de tipos de consulta.  
  
 **Painel Grade**  
 Exibe os objetos referenciados pela consulta em uma grade. Você pode usar este painel para adicionar e remover colunas da consulta e alterar as configurações de cada coluna.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
 **Painel SQL**  
 Exibe a consulta como uma instrução SQL. Digite para alterar a instrução SQL da consulta.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
 **Painel de resultados**  
 Exibe os resultados da consulta quando você clica em **Executar** no painel **Barra de Ferramentas** .  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
