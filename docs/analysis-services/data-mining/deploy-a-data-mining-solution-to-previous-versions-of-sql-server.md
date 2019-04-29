---
title: Implantar uma solução de mineração de dados em versões anteriores do SQL Server | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df527197f0ddd1eacc2e86e59092f45b1ac78c9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011020"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>Implantar uma solução de mineração de dados em versões anteriores do SQL Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Esta seção descreve problemas de compatibilidade conhecidos que podem surgir durante a tentativa de implantação de um modelo ou estrutura de mineração de dados criado em uma instância do [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] para um banco de dados que usa o SQL Server 2005 Analysis Services, ou quando você implanta modelos criados no SQL Server 2005 em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 A implantação em uma instância do SQL Server 2000 Analysis Services não é suportada.  
  
 [Implantando modelos de série temporal](#bkmk_TimeSeries)  
  
 [Implantando modelos com controle](#bkmk_Holdout)  
  
 [Implantando modelos com filtros](#bkmk_Filter)  
  
 [Restaurando de backups de banco de dados](#bkmk_Backup)  
  
 [Usando a sincronização de banco de dados](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> Implantando modelos de série temporal  
 O algoritmo MTS foi aprimorado no SQL Server 2008 com a adição de um segundo algoritmo complementar, o ARIMA. Para obter mais informações sobre as alterações no algoritmo de série temporal, consulte [Algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
 Portanto, os modelos de mineração de série temporal que usam o novo algoritmo ARIMA podem apresentar um comportamento diferente quando implantados em uma instância do SQL Server 2005 Analysis Services.  
  
 Se você tiver definido explicitamente o parâmetro PREDICTION_SMOOTHING para controlar a mistura dos modelos ARTXP e ARIMA na previsão, ao implantar este modelo em uma instância do SQL Server 2005, o Analysis Services gerará um erro declarando que o parâmetro não é válido. Para impedir esse erro, exclua o parâmetro PREDICTION_SMOOTHING e converta os modelos em um puro modelo ARTXP.  
  
 Por outro lado, se você implantar um modelo de série temporal que foi criado com o SQL Server 2005 Analysis Services em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ao abrir o modelo de mineração do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], os arquivos de definição serão primeiramente convertidos no novo formato e dois novos parâmetros serão adicionados, por padrão, a todos os modelos de série temporal. O parâmetro FORECAST_METHOD é adicionado com o valor padrão de MIXED e o parâmetro PREDICTION_SMOOTHING é adicionado com o valor padrão de 0,5. Porém, o modelo continuará usando apenas ARTXP para fazer previsões até que o modelo seja reprocessado. Assim que você reprocessa o modelo, a previsão muda para usar ARIMA e ARTXP.  
  
 Desse modo, se deseja evitar a alteração do modelo, apenas procure e nunca processe o modelo. Se preferir, defina explicitamente os parâmetros FORECAST_METHOD ou PREDICTION_SMOOTHING.  
  
 Para obter informações detalhadas sobre como configurar modelos mistos, consulte [Referência técnica do algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Se o provedor usado para a fonte de dados do modelo for SQL Client Data Provider 10, você também deve modificar a definição de fonte de dados para especificar a versão anterior do SQL Server Native Client. Caso contrário, o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] gera um erro que declara que o provedor não é registrado.  
  
##  <a name="bkmk_Holdout"></a> Implantando modelos com controle  
 Se você criar uma estrutura de mineração que contém uma partição de validação usada para testar modelos de mineração de dados, a estrutura de mineração pode ser implantada em uma instância do SQL Server 2005, mas as informações de partição serão perdidas.  
  
 Ao abrir a estrutura de mineração no SQL Server 2005 Analysis Services, o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] gera um erro e, em seguida, gera novamente a estrutura para remover a partição de controle.  
  
 Depois que a estrutura é recriada, o tamanho da partição de exibição não está mais disponível na janela Propriedades. No entanto, o valor \<ddl100_100:HoldoutMaxPercent > 30\</ddl100_100:HoldoutMaxPercent >) ainda podem estar presentes no arquivo de script ASSL.  
  
##  <a name="bkmk_Filter"></a> Implantando modelos com filtros  
 Se você aplicar um filtro a um modelo de mineração, o modelo pode ser implantado em uma instância do SQL Server 2005, mas o filtro não será aplicado.  
  
 Quando você abre o modelo de mineração, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera um erro e, em seguida, gera novamente o modelo para remover o filtro.  
  
##  <a name="bkmk_Backup"></a> Restaurando de backups de banco de dados  
 Você não pode restaurar um backup de banco de dados que foi criado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para uma instância do SQL Server 2005. Se fizer isso, o SQL Server Management Studio gerará um erro.  
  
 Se você criar um backup de um banco de dados do SQL Server 2005 Analysis Services e restaurar esse backup em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], todos os modelos de série temporal serão modificados conforme descrito na seção anterior.  
  
##  <a name="bkmk_Synch"></a> Usando a sincronização de banco de dados  
 A sincronização do banco de dados não tem suporte do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o SQL Server 2005.  
  
 Se você tentar sincronizar um banco de dados [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o servidor retornará um erro e a sincronização do banco de dados falhará.  
  
## <a name="see-also"></a>Consulte também  
 [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md)  
  
  
