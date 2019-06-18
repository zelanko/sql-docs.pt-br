---
title: Definir opções de processamento (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 986ae6e89727b0cef59e4d6b3bf7e5d92bd5342b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580545"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Definir opções de processamento (Reporting Services no modo integrado do SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Defina as opções de processamento em um relatório do Reporting Services para determinar quando ocorre o processamento de dados. Pode também definir um valor de tempo limite para o processamento de relatórios, além de opções que determinam se o histórico de relatórios está habilitado para o relatório atual.  
  
-   Você pode executar um relatório como instantâneo de relatório para evitar que o relatório seja executado em momentos arbitrários (durante um backup agendado, por exemplo). Um instantâneo de relatório normalmente é criado e, em seguida, atualizado de acordo com um agendamento, permitindo marcar o horário exato em que ocorrerá o processamento de dados e do relatório. Se um relatório basear-se em consultas cujo processamento seja demorado ou que utilizem dados de uma fonte de dados que prefira que não seja acessada durante determinadas horas, você deverá executar o relatório como instantâneo.  
  
-   Um servidor de relatório pode armazenar em cache uma cópia de um relatório processado e devolvê-la quando um usuário abrir o relatório. O armazenamento em cache é uma técnica de aprimoramento de desempenho. O armazenamento em cache pode diminuir o tempo necessário para recuperar um relatório, caso ele seja grande ou acessado frequentemente.  
  
-   Um histórico de relatórios é uma coleção de cópias de um relatório executadas anteriormente. É possível usar o histórico de relatórios para manter ao longo do tempo um registro de um relatório. Um histórico de relatórios não se destina a relatórios que contenham dados confidenciais ou pessoais. Por este motivo, um histórico de relatórios pode incluir somente os relatórios que consultem uma fonte de dados utilizando um conjunto único de credenciais (armazenadas ou usadas para a execução de um relatório de forma autônoma) disponível para todos os usuários que executem um relatório.  

    A integração do Reporting Services com o SharePoint utiliza recursos de gerenciamento de inserção e extração de conteúdo do SharePoint para salvar atualizações em tipos de conteúdo do Reporting Services. isso inclui a criação de instantâneos de relatórios. Portanto, se você ativou o controle de versões em uma biblioteca de documentos, verá a versão de relatório atualizada quando um novo instantâneo de histórico de relatórios for criado. Esse é um efeito colateral de atualizar instantâneos. Quando um instantâneo é atualizado, ele faz com que a propriedade LastExecution do relatório se altere, e isso causa uma alteração na versão do relatório.  

-   Você pode especificar valores de tempo limite para definir limites para o uso dos recursos do sistema.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="set-data-refresh-options"></a>Definir opções de atualização de dados
  
1.  Aponte para um relatório na biblioteca.  
  
2.  Clique na seta para baixo e selecione **Gerenciar opções de processamento**.  
  
3.  Em **Opções de Atualização de Dados**, clique em **Usar dados de instantâneo**. Se você vir a mensagem " Este relatório não pode ser executado a partir de um instantâneo porque uma ou mais das credenciais de fontes de dados não estão armazenadas", isto significa que o relatório não está configurado para ser executado de forma autônoma e que você deve modificar as fontes de dados para usar credenciais armazenadas antes de definir esta opção.  
  
4.  Em **Opções de Instantâneo de Dados**, selecione **Agendar processamento de dados**.  
  
5.  Selecione **Em uma agenda compartilhada** se você tiver uma agenda compartilhada que deseje usar; caso contrário, clique em **Em uma agenda personalizada**e em **Configurar**.  
  
6.  Selecione a frequência, o agendamento, as datas de início e término e clique em **OK**.  
  
7.  Em **Opções de Instantâneo de Dados**, selecione **Criar ou atualizar o instantâneo quando esta página for salva** se você quiser criar imediatamente dados de instantâneo para serem usados com o relatório, sem aguardar o processamento de dados agendado.  
  
## <a name="set-report-caching-options"></a>Definir opções de cache de relatório
  
1.  Aponte para um relatório na biblioteca.  
  
2.  Clique na seta para baixo e selecione **Gerenciar opções de processamento**.  
  
3.  Em **Opções de Atualização de Dados**, clique em **Usar dados armazenados em cache**. Se você vir a mensagem "Não é possível armazenar este relatório em cache porque uma ou mais das credenciais de fonte de dados não estão armazenadas", isto significa que o relatório não está configurado para ser executado de forma autônoma e que você deve modificar as fontes de dados para usar credenciais armazenadas antes de definir esta opção.  
  
4.  Em **Opções de Cache**, especifique como o cache expirará:  
  
    -   Insira um número de minutos após o qual o cache expirará.  
  
    -   Use uma agenda compartilhada para limpar o cache nos horários especificados na agenda.  
  
    -   Crie uma agenda compartilhada para limpar o cache em um horário especificado por você.  
  
## <a name="set-processing-time-out-values"></a>Definir valores de tempo limite de processamento
  
1.  Aponte para um relatório na biblioteca.  
  
2.  Clique na seta para baixo e selecione **Gerenciar opções de processamento**.  
  
3.  Em **Tempo Limite de Processamento**, selecione **Usar a configuração padrão do site** se você quiser usar o valor especificado no nível do servidor de relatório. Caso contrário, selecione **Não especificar tempo limite para processamento de relatório** ou **Limitar o processamento de relatórios em segundos** se quiser substituir esse valor para que não haja tempo limite ou para que haja outros valores de tempo limite.  
  
## <a name="set-report-history-options-and-limits"></a>Definir opções e limites de histórico de relatórios
  
1.  Aponte para um relatório na biblioteca.  
  
2.  Clique na seta para baixo e selecione **Gerenciar opções de processamento**.  
  
3.  Em **Opções de Instantâneo de Histórico**, especifique como e quando o processamento de dados ocorre e é salvo.  
  
4.  Em **Limites de Instantâneo de Histórico**, selecione **Usar a configuração padrão do site** se desejar usar o valor especificado no nível do servidor de relatório. Caso contrário, selecione **Não limitar o número de instantâneos** ou **Limitar o número de instantâneos** para especificar um valor personalizado.  
  
## <a name="set-database-timeout"></a>Definir tempo limite de banco de dados
  
*  Use o Windows PowerShell para definir o tempo limite de banco de dados de um servidor de relatório do SharePoint. Para obter mais informações, confira a seção "Obter e definir Propriedades do banco de dados do aplicativo de serviço de relatório" de [Cmdlets do PowerShell para o modo do SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="next-steps"></a>Próximas etapas

 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Armazenar relatórios em cache](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
