---
title: "Limites de tamanho de relatório e instantâneo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- large reports
- maximum report size
- size [SQL Server], reports
- report size [Reporting Services]
- reports [Reporting Services], size
- denial of service attacks [Reporting Services]
ms.assetid: 1e3be259-d453-4802-b2f5-6b81ef607edf
caps.latest.revision: "48"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d433a0ea0b586929858ca4fe83fcf1a48274f59e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="report-and-snapshot-size-limits"></a>Limites de tamanho do relatório e do instantâneo
  Os administradores que gerenciam uma implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem usar as informações deste tópico para entender os limites de tamanho de relatório quando este é publicado em um servidor de relatório, renderizado em tempo de execução e salvo no sistema de arquivos. Este tópico também fornece uma orientação prática sobre como medir o tamanho de um banco de dados do servidor de relatório e descreve o efeito do tamanho do instantâneo no desempenho do servidor.  
  
## <a name="maximum-size-for-published-reports"></a>Tamanho máximo para relatórios publicados  
 No servidor de relatório, o tamanho do relatório e do modelo baseia-se nos arquivos de definição de relatório (.rdl) e de modelo de relatório (.smdl) publicados no servidor. O servidor de relatório não limita o tamanho de um relatório publicado. Porém, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] impõe um tamanho máximo para itens que são postados no servidor. Por padrão, esse limite é 4 megabytes (MB). Se um arquivo que ultrapassa esse limite for transferido ou publicado em um servidor de relatório, ocorrerá uma exceção HTTP. Neste caso, modifique o padrão aumentando o valor do elemento **maxRequestLength** no arquivo Machine.config.  
  
 Embora um modelo de relatório possa ser muito grande, definições de relatório raramente excedem 4 MB. Um tamanho de relatório mais comum é da ordem de quilobytes (KB). No entanto, se imagens inseridas forem incluídas, a codificação dessas imagens pode resultar em grandes definições de relatório que ultrapassam o padrão de 4 MB.  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] impõe um limite máximo em arquivos postados para reduzir a ameaça de ataques de negação de serviço contra o servidor. Aumentar o valor do limite superior destorce algumas proteções fornecidas por esse limite. Aumente o valor somente se você tiver certeza de que o benefício de fazer isso supera qualquer risco de segurança adicional.  
  
 Lembre-se de que o valor definido para o elemento **maxRequestLength** deve ser maior que os limites de tamanho reais que você deseja impor. Você precisa aumentar o valor para dar conta do aumento inevitável no tamanho da solicitação HTTP que ocorre depois que todos os parâmetros são encapsulados em um envelope SOAP, e a codificação Base64 é aplicada a determinados. A codificação Base64 aumenta o tamanho dos dados originais em aproximadamente 33%. Consequentemente, o valor que você especifica para o elemento **maxRequestLength** precisa ser aproximadamente 33% maior que o tamanho real utilizável do item. Por exemplo, se você especificar um valor de 64 MB para **maxRequestLength**, na verdade poderá esperar o tamanho máximo de aproximadamente 48 MB para os arquivos de relatório que são postados no servidor de relatório.  
  
## <a name="report-size-in-memory"></a>Tamanho do relatório na memória  
 Quando você executa um relatório, o tamanho do relatório é igual à quantidade de dados retornados no relatório mais o tamanho do fluxo de saída. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não impõe um limite máximo para o tamanho de um relatório renderizado. A memória do sistema determina o limite superior do tamanho (por padrão, um servidor de relatório usa toda a memória configurada disponível ao renderizar um relatório), mas é possível especificar configurações para definir os limites e as diretrizes de gerenciamento da memória. Para obter mais informações, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
 Para qualquer relatório, o tamanho pode variar consideravelmente dependendo da quantidade de dados retornados e do formato de renderização usado para o relatório. Um relatório parametrizado pode ser maior ou menor dependendo de como os valores de parâmetro afetam os resultados de consulta. O formato de saída escolhido afeta o tamanho do relatório dos seguintes modos:  
  
-   HTML processa uma página do relatório de cada vez. Como o relatório é processado em unidades menores, menos memória é necessária para processar blocos específicos.  
  
-   PDF, Excel, TIFF, XML e CSV processam o relatório inteiro na memória antes de exibir o relatório para o usuário.  
  
 Para medir o tamanho de um relatório renderizado, você pode exibir o log de execução de relatório. Para obter mais informações, veja [ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 Para calcular o tamanho de um relatório renderizado no disco, você pode exportar e salvar o relatório no sistema de arquivos (o arquivo salvo inclui dados e informações de formatação do relatório).  
  
 O único limite fixo do tamanho do relatório é determinado durante a renderização em formato Excel. As planilhas não podem ter mais de 65536 linhas ou 256 colunas. Outros formatos de renderização não têm esses limites, de modo que o tamanho é limitado somente pela quantidade de recursos do servidor.  
  
> [!NOTE]  
>  O processamento e a renderização do relatório ocorrem na memória. Se houver grandes relatórios ou um grande número de usuários, faça algum tipo de planejamento de capacidade para ter certeza de que a implantação do servidor de relatório seja executada em um nível satisfatório para os usuários. Para obter mais informações sobre ferramentas e diretrizes, consulte as seguintes publicações no MSDN: [Planning for Scalability and Performance with Reporting Services (Planejamento de escalabilidade e desempenho com o Reporting Services)](http://go.microsoft.com/fwlink/?LinkID=70650) e [Using Visual Studio 2005 to Perform Load Testing on a SQL Server 2005 Reporting Services Report Server (Usando o Visual Studio 2005 para realizar o teste de carga em um servidor de relatórios do Reporting Services do SQL Server 2005)](http://go.microsoft.com/fwlink/?LinkID=77519).  
  
## <a name="measuring-snapshot-storage"></a>Medindo o armazenamento de instantâneos  
 O tamanho de qualquer instantâneo é diretamente proporcional à quantidade de dados no relatório. Os instantâneos normalmente são muito maiores que outros itens armazenados em um servidor de relatório. O tamanho do instantâneo varia, em geral, de alguns megabytes a dezenas de megabytes. Se você tiver relatórios muito grandes, espere para ver instantâneos que são ainda muito maiores. Dependendo da frequência de uso dos instantâneos e da configuração do histórico de relatórios, a quantidade de espaço em disco necessária para o banco de dados do servidor de relatório pode aumentar rapidamente em um curto período de tempo.  
  
 Por padrão, os bancos de dados **reportserver** e **reportservertempdb** são definidos como autogrow. Embora o tamanho do banco de dados possa aumentar automaticamente, nunca é diminuído automaticamente. Se o banco de dados **reportserver** tiver um excesso de capacidade devido à exclusão de instantâneos, reduza-o manualmente para recuperar o espaço em disco. Similarmente, se **reportservertempdb** tiver aumentado para acomodar um volume extremamente grande de relatórios interativos, a alocação do espaço em disco permanecerá nessa configuração até ser diminuída.  
  
 Para medir o tamanho dos bancos de dados do servidor de relatório, execute os seguintes comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] . O cálculo do tamanho total do banco de dados em intervalos regulares pode ajudar você a desenvolver estimativas razoáveis de como alocar espaço para o banco de dados do servidor de relatórios com o passar do tempo. As seguintes instruções medem a quantidade de espaço usada atualmente (as instruções supõem que você está usando os nomes padrão de banco de dados):  
  
```  
USE ReportServer  
EXEC sp_spaceused  
```  
  
## <a name="snapshot-size-and-report-server-performance"></a>Tamanho do instantâneo e desempenho do servidor de relatório  
 O tamanho do instantâneo afeta o desempenho do servidor quando o relatório é processado e renderizado. O desempenho do servidor é afetado principalmente pelas operações de renderização; portanto, se houver um grande instantâneo, haverá algum atraso quando os usuários solicitarem o relatório. Dependendo do número de usuários, você pode esperar atrasos quando o tamanho do instantâneo for maior do que 100 megabytes.  
  
 Para minimizar os atrasos de desempenho devido a instantâneos grandes, faça o seguinte:  
  
-   Implante o servidor de relatório e o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] em computadores separados.  
  
-   Adicione mais memória ao sistema.  
  
-   Releia o documento “Planejando a escalabilidade e o desempenho em serviços de relatório” no site do MSDN para obter as práticas recomendadas sobre como configurar um servidor de relatório para a empresa.  
  
 A quantidade de instantâneos que são armazenados em um banco de dados do servidor de relatório não é, por si só, um fator de desempenho. Você pode armazenar um número grande de instantâneos sem afetar o desempenho do servidor. Os instantâneos podem ser mantidos indefinidamente. Porém, verifique se o histórico de relatórios pode ser configurado. Se o administrador de um servidor de relatório diminuir o limite do histórico, os relatórios do histórico que você pretende manter podem ser perdidos. Se você excluir o relatório, todo o histórico relacionado será excluído também.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Processar relatórios grandes](../../reporting-services/report-server/process-large-reports.md)  
  
  
