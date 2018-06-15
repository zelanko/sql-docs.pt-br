---
title: Limpar os Caches do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ed87e37ca9b13af696977a86eeccd34eec81e87
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016553"
---
# <a name="clear-the-analysis-services-caches"></a>Limpar os caches do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O Analysis Services armazena dados em cache dados para melhorar o desempenho da consulta. Este tópico fornece recomendações para usar o comando XMLA ClearCache para limpar caches que foram criados em resposta a uma consulta MDX. Os efeitos da execução de ClearCache variam dependendo se você está usando um modelo tabular ou multidimensional.  
  
 **Quando limpar o cache de modelos multidimensionais**  
  
 Em bancos de dados multidimensionais, o Analysis Services compila caches no mecanismo de fórmula ao avaliar um cálculo e no mecanismo de armazenamento para os resultados de consultas de dimensões e de grupos de medidas. Consultas de grupos de medidas ocorrem quando o mecanismo de fórmula precisa de dados de medida para uma coordenada de célula ou subcubo. Consultas de dimensão ocorrem ao consultar hierarquias não naturais e ao aplicar autoexists.  
  
 É recomendável limpar o cache para executar testes de desempenho. Limpando o cache entre execuções de teste, você assegura que o cache não irá distorcer os resultados dos testes que avaliam o impacto de uma alteração de design de consulta.  
  
 **Quando limpar o cache de modelos tabulares**  
  
 Geralmente, os modelos tabulares são armazenados na memória, quando agregações e outros cálculos são realizados no momento em que uma consulta é executada. Como tal, o comando ClearCache tem um efeito limitado sobre os modelos tabulares. Em um modelo tabular, os dados podem ser adicionados aos caches do Analysis Services se as consultas MDX forem executadas com base nesses dados. Em particular, as medidas DAX referidas pelas operações MDX e autoexist podem armazenar os resultados no cache de fórmulas e no cache de dimensão respectivamente. No entanto, observe que hierarquias não naturais e consultas de grupos de medidas não armazenam resultados em cache no mecanismo de armazenamento. Além disso, é importante reconhecer que as consultas DAX não armazenam os resultados em cache no mecanismo de fórmula e armazenamento. Enquanto o cache existir em resultado de consultas MDX, a execução do comando ClearCache em um modelo tabular invalidará os dados armazenados em cache do sistema.  
  
 Executar o comando ClearCache também limpa os caches no mecanismo analítico na memória xVelocity (VertiPaq). O mecanismo xVelocity mantém um pequeno conjunto de resultados em cache. Executar o comando ClearCache invalida esses caches no mecanismo xVelocity.  
  
 Por fim, executar o comando ClearCache também remove dados residuais deixados na memória quando um modelo tabular é reconfigurado para o modo **DirectQuery** . Isso é particularmente importante quando o modelo contém dados confidenciais sujeitos a controles rígidos. Nesse caso, executar o comando ClearCache é uma ação de precaução que você pode executar para garantir que os dados confidenciais constem somente onde desejado. É necessário limpar o cache manualmente quando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] é usado para implantar o modelo e alterar o modo de consulta. Em contrapartida, usar o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para especificar **DirectQuery** no modelo e em partições limpa automaticamente o cache ao mudar o modelo a ser usado nesse modo de consulta.  
  
 Em comparação com recomendações para limpar os caches de modelos multidimensionais durante os testes de desempenho, não há uma recomendação ampla para limpar os caches de modelos tabulares. Se você não for gerenciar a implantação de um modelo tabular que contém dados confidenciais, não haverá uma tarefa administrativa específica que exija a limpeza do cache.  
  
## <a name="clear-the-cache-for-analysis-services-models"></a>Limpar o cache de modelos do Analysis Services  
 Para limpar o cache, use o XMLA e o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode limpar o cache no nível de banco de dados, cubo, dimensão, tabela ou grupo de medidas. As etapas a seguir para limpar o cache no nível de banco de dados aplicam-se aos modelos multidimensionais e tabulares.  
  
> [!NOTE]  
>  Testes de desempenho rigorosos podem exigir uma abordagem mais abrangente para limpar o cache. Para obter instruções sobre como liberar o Analysis Services e os caches do sistema de arquivos, consulte a seção sobre limpeza de caches no [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?linkID=http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Nos modelos multidimensionais e tabulares, limpar alguns desses caches pode envolver duas etapas que consistem em invalidar o cache na execução do comando ClearCache e esvaziar o cache quando a próxima consulta é recebida. A redução no consumo de memória ficará evidente somente depois que o cache for esvaziado de fato.  
  
 É necessário fornecer um identificador de objeto à instrução **ClearCache** na consulta XMLA para limpar o cache. A primeira etapa deste tópico explica como obter um identificador de objeto.  
  
#### <a name="step-1-get-the-object-identifier"></a>Etapa 1: obter o identificador de objeto  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse em um objeto, selecione **Propriedades**e copie o valor da propriedade da ID no painel **Propriedades** . Essa abordagem funciona para banco de dados, cubo, dimensão ou tabela.  
  
2.  Para obter a ID do grupo de medidas, clique com o botão direito do mouse no grupo de medidas e selecione **Script de Grupo de Medidas como**. Escolha **Criar** ou **Alterar**e envie a consulta para uma janela. A ID do grupo de medidas ficará visível na definição do objeto. Copie a ID da definição do objeto.  
  
#### <a name="step-2-run-the-query"></a>Etapa 2: executar a consulta  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse em um banco de dados, aponte para **Nova Consulta**e selecione **XMLA**.  
  
2.  Copie o exemplo de código a seguir na janela de consulta XMLA. Altere **DatabaseID** para a ID do banco de dados na conexão atual.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     Opcionalmente, você pode especificar o caminho de um objeto filho, como um grupo de medidas, para limpar o cache apenas desse objeto.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  Pressione F5 para executar a consulta. Você deverá obter o seguinte resultado:  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  
