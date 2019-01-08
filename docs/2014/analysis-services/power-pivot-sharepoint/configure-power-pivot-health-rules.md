---
title: Regras de integridade do PowerPivot - configurar | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a01e63e6-97dc-43e5-ad12-ae6580afc606
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f96a4b976d338e7f005d0f731bac0b58f5798bb
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401471"
---
# <a name="powerpivot-health-rules---configure"></a>Regras de integridade do PowerPivot - Configurar
  O PowerPivot para SharePoint inclui regras de integridade do SharePoint que o ajudam a monitorar e solucionar problemas de disponibilidade e configuração do servidor. Regras de integridade que se aplicam ao PowerPivot para SharePoint aparecem na página Revisar definições de regra.  
  
 Regras de integridade fornecem a detecção de problemas de servidor que podem acabar resultando em interrupções de serviço. O PowerPivot para SharePoint fornece vários regras para ajudá-lo a identificar e corrigir problemas antes que afetem seus usuários. Você pode personalizar muitas destas regras para ajustá-las às características exclusivas de sua implantação. Por exemplo, se você desejar mais tempo para tratar de avisos sobre espaço em disco, poderá aumentar o percentual de espaço disponível em disco de 5% para 10% de forma que receba o aviso mais cedo.  
  
 Regras que podem ser personalizadas são aquelas que relatam o consumo de recursos ou a disponibilidade do servidor. A personalização é útil nestas áreas porque a capacidade do sistema subjacente varia muito de acordo com o servidor e a topologia de implantação. Em contraste, nenhuma personalização está disponível para regras que identificam problemas na configuração de servidor ou problemas de segurança. Essas regras devem ser aplicadas uniformemente em todas as instalações.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Observação:** As definições de regra de integridade são configuradas separadamente para a instância do SQL Server Analysis Services e o aplicativo de serviço PowerPivot. Use as instruções neste tópico para configurar as regras de integridade para cada serviço. Para uma implantação do SharePoint 2013, o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] usa apenas o aplicativo de serviço. Portanto, o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instala diferentes conjuntos de regras de integridade para diferentes versões do SharePoint. Consulte a coluna "versão" no tópico [referência de regras de integridade &#40;PowerPivot para SharePoint&#41;](health-rules-reference-power-pivot-for-sharepoint.md), ou você pode executar o seguinte comando do Windows PowerShell para ver as regras instaladas.  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like "*power*"}  | format-table -property * -autosize | out-default  
```  
  
 **Neste tópico:**  
  
 [Exibir regras de integridade do PowerPivot](#bkmk_view)  
  
 [Configurar regras de integridade usadas para avaliar a estabilidade do servidor (SQL Server Analysis Services)](#bkmk_HR_SSAS)  
  
 [Configurar regras de integridade usadas para avaliar a estabilidade do aplicativo (aplicativo de serviço PowerPivot)](#bkmk_evaluate_application_stability)  
  
## <a name="prerequisites"></a>Prerequisites  
 Você deve ser um administrador de aplicativo de serviço para alterar propriedades de configuração da instância do Analysis Services e do aplicativo de serviço PowerPivot.  
  
##  <a name="bkmk_view"></a> Exibir regras de integridade do PowerPivot  
  
1.  Na Administração Central do SharePoint, clique em **Monitoramento**e, na seção **Analisador de Integridade** , clique em **Revisar definições de regra**.  
  
2.  Na seção Configuração, localize as regras com o prefixo **PowerPivot:** . Todas as regras de integridade relacionadas ao PowerPivot têm este prefixo para ajudar a diferenciá-las das regras internas do SharePoint.  
  
 Estas regras aparecerão na página **Rever problemas e soluções** quando forem detectados problemas.  
  
 Se você suspeitar de um problema que deseja investigar imediatamente, poderá executar uma verificação de regra manualmente para descobrir se existe um problema.  
  
 Para fazer isso, clique na regra para abrir sua definição de regra e clique em **Executar Agora** . Clique em **Fechar** para voltar para a página **Rever problemas e soluções** para exibir o relatório. Se a regra detectou um problema, um aviso ou erro será reportado na página. Em alguns casos, pode levar alguns minutos antes de o erro ou aviso ser exibido.  
  
##  <a name="bkmk_HR_SSAS"></a> Configurar regras de integridade usadas para avaliar a estabilidade do servidor (SQL Server Analysis Services)  
 A instância do Analysis Services inclui regras de integridade que detectam problemas em nível de sistema (CPU, memória e espaço em disco usado para fins de cache). Use as instruções a seguir para modificar limites que disparam regras de integridade específicas.  
  
1.  Na Administração Central do SharePoint, na seção **Configurações do Sistema** , clique em **Gerenciar serviços no servidor**.  
  
2.  Na parte superior da página, selecione o servidor em seu farm do SharePoint que tem uma instância do Analysis Services (na ilustração a seguir, o nome de servidor é AW-SRV033). O**SQL Server Analysis Services** aparecerá na lista de serviços.  
  
     ![Captura de tela de gerenciar serviços na página do servidor](../media/ssas-centraladmin-servicesonserver.gif "captura de tela de gerenciar serviços na página do servidor")  
  
3.  Clique **SQL Server Analysis Services**.  
  
4.  Nas páginas de propriedades de serviço, nas Configurações de Regra de Integridade, modifique as seguintes configurações:  
  
     Alocação insuficiente de recursos da CPU (o padrão é 80%)  
     Esta regra de integridade será disparada se os recursos de CPU usados pelo processo de servidor do Analysis Services (msmdsrv.exe) permanecer em 80% ou acima por um período de 4 horas (conforme especificado pela configuração de Intervalo de Coleta de Dados).  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: Analysis Services não tem recursos suficientes de CPU para executar as operações solicitadas.**  
  
     Recursos insuficientes da CPU no sistema (o padrão é 90%)  
     Esta regra de integridade será disparada se os recursos da CPU para o servidor permanecerem em 90% ou acima por mais de 4 horas (conforme especificado pela configuração do Intervalo de Coleta de Dados). A utilização de CPU global é medida como parte do algoritmo de balanceamento de carga baseado em integridade que monitora o uso da CPU como uma medida da integridade de servidor.  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: Em geral, o uso da CPU é muito alto.**  
  
     Limite de memória insuficiente (o padrão é 5%)  
     Em um servidor de aplicativos do SharePoint, uma instância do SQL Server Analysis Services deve ter sempre uma pequena quantidade de memória reservada que nunca é usada. Como o servidor é associado à memória na maioria de suas operações, o servidor apresenta execução melhor quando não é executado no limite máximo. Os 5% de memória não usados são calculados como um percentual de memória alocada para o Analysis Services. Por exemplo, se você tiver 200 GB de memória total, e for alocado 80% (ou 160 GB) para o Analysis Services, os 5% de memória não usada serão 5% de 160 GB (ou 8 GB).  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: Analysis Services não tem memória suficiente para executar as operações solicitadas.**  
  
     Número máximo de conexões (o padrão é 100).  
     Esta regra de integridade será disparada se o número de conexões para a instância do Analysis Services permanecer em ou acima de 100 conexões por um período de 4 horas (conforme especificado pela configuração de Intervalo de Coleta de Dados). Este valor padrão é arbitrário (não é baseado nas especificações de hardware de seu servidor ou na atividade do usuário), portanto, você pode aumentá-lo ou abaixá-lo dependendo da capacidade do servidor e da atividade do usuário em seu ambiente.  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: O número alto de conexões indica que mais servidores devem ser implantados para tratar a carga atual.**  
  
     Espaço insuficiente em disco (o padrão é 5%)  
     O espaço em disco é usado para armazenar em cache os dados PowerPivot cada vez que o banco de dados é solicitado. Esta regra permite conhecer quando o espaço em disco é insuficiente. Por padrão, esta regra de integridade é disparada quando o espaço em disco é inferior a 5% na unidade de disco onde a pasta de backup está localizada. Para obter mais informações sobre o uso do disco, consulte [configurar o uso de espaço em disco &#40;PowerPivot para SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md).  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: Espaço em disco é insuficiente na unidade onde os dados do PowerPivot é armazenado em cache.**  
  
     Intervalo de coleta de dados (em horas)  
     Você pode especificar o período de coleta de dados usado para calcular os números usados para disparar regras de integridade. Embora o sistema seja constantemente monitorado, os limites usados para disparar avisos de regra de integridade são calculados usando dados que foram gerados em um intervalo predefinido. O intervalo padrão é 4 horas. O servidor recupera os dados de sistema e uso coletados durante as 4 horas anteriores para avaliar o número de conexões de usuário, uso de espaço em disco, e taxas de CPU e de utilização de memória.  
  
##  <a name="bkmk_evaluate_application_stability"></a> Configurar regras de integridade usadas para avaliar a estabilidade do aplicativo (aplicativo de serviço PowerPivot)  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na página Aplicativos de Serviço, clique em **Aplicativo de Serviço PowerPivot Padrão**.  
  
     ![Captura de tela da página Gerenciar aplicativo](../media/ssas-centraladmin-app.gif "captura de tela da página Gerenciar aplicativo")  
  
3.  O Painel de Gerenciamento do PowerPivot é exibido. Clique em **Configurar parâmetros do aplicativo de serviço** na lista **Ações** para abrir a página de configurações de aplicativo de serviço.  
  
     ![Captura de tela do painel, concentre-se na lista de ações](../media/ssas-centraladmin-actionslist.gif "captura de tela do painel, concentre-se na lista de ações")  
  
4.  Em Configurações de Regra de Integridade, modifique as seguintes configurações:  
  
     Taxa de conexão de carregamento (o padrão é 20%)  
     Esta regra de integridade será disparada se o número de eventos de carga for alto em relação ao número de eventos de conexão, sinalizando que o servidor pode estar descarregando bancos de dados muito rapidamente, ou que essas configurações de redução de cache são muito agressivas.  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: A taxa de eventos de carga para conexões é muito alta.**  
  
     Intervalo de coleta de dados (o padrão é 4 horas)  
     Você pode especificar o período de coleta de dados usado para calcular os números usados para disparar regras de integridade. Embora o sistema seja constantemente monitorado, os limites usados para disparar avisos de regra de integridade são calculados usando dados que foram gerados em um intervalo predefinido. O intervalo padrão é 4 horas. O servidor recupera os dados de sistema e uso coletados durante as 4 horas anteriores para avaliar a carga para a taxa de coleção.  
  
     Verifique as atualizações para o PowerPivot Management Dashboard.xlsx (o padrão é 5 dias)  
     O arquivo PowerPivot Management Dashboard.xlsx é uma fonte de dados usada por relatórios no Painel de Gerenciamento do PowerPivot. Em uma configuração de servidor padrão, o arquivo .xlsx é atualizado diariamente, usando dados de uso coletados pelo SharePoint e o Serviço do Sistema PowerPivot. No caso de o arquivo não ser atualizado, uma regra de integridade reporta isso como um problema. Por padrão, a regra será disparada se o carimbo de data/hora do arquivo não tiver sido alterado durante 5 dias.  
  
     Para obter mais informações sobre a coleta de dados de uso, consulte [configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
     Essa configuração corresponde à definição de regra a seguir sobre o **rever problemas e soluções** página: **PowerPivot: Dados de uso não são atualizados com a frequência esperada.**  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o uso de espaço em disco &#40;PowerPivot para SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)   
 [Painel de Gerenciamento PowerPivot e dados de uso](power-pivot-management-dashboard-and-usage-data.md)  
  
  
