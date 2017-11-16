---
title: "Configurar e exibir o log de diagnóstico e SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 85f62d29-cdc6-45b3-be1f-ff1182939858
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e94ef1aeee4d633353964a6398bd12b89ef86cf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="configure-and-view-sharepoint-and-diagnostic-logging"></a>Configurar e exibir o log de diagnóstico e SharePoint
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] são registrados em arquivos de log do SharePoint. Use as informações deste tópico para configurar informações de níveis de log e do arquivo de log de exibição. Você pode controlar quais eventos de servidor do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] são registrados em log no arquivo. Você também pode controlar a severidade de mensagens que são registradas em log. Para obter mais informações, consulte [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Neste tópico:  
  
-   [Local do Arquivo de Log](#bkmk_filelocation)  
  
-   [Modifique os níveis de registro em log de diagnóstico para categorias de evento individuais](#bkmk_modifyloglevels)  
  
-   [Como exibir arquivos de log do SharePoint](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> Local do Arquivo de Log  
 Por padrão, os arquivos de log do SharePoint são salvos no seguinte local:  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 A pasta LOGS contém arquivos de log (`.log`), arquivos de dados (`.txt`) e arquivos de uso (`.usage`). A convenção de nomenclatura de arquivo para um log de rastreamento do SharePoint é o nome de servidor seguido por um carimbo de data/hora. São criados logs de rastreamento de SharePoint em intervalos normais e sempre que há um IISRESET. É comum que haja muitos logs de rastreamento dentro de um período de 24 horas.  
  
##  <a name="bkmk_modifyloglevels"></a> Modifique os níveis de registro em log de diagnóstico para categorias de evento individuais  
 Por padrão, o registro em log ULS dos eventos do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] é definido como *Meio*. Esta configuração é nova para o SQL Server 2012. Se você atualizou um servidor da versão anterior, o nível de log ainda poderia ser definido como *Detalhado*, o nível padrão no SQL Server 2008 R2. Se você estiver acostumado a revisar os logs de ULS para obter informações de uso do servidor do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , notará que, como resultado desta alteração, há menos informações sobre operações de servidor do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
 Tirando as exceções, que são do tipo *Alta*, todas as mensagens de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] entram na categoria Detalhado. Se você quiser entradas de log para operações de servidor rotineiras como conexões, solicitações ou relatório de consulta, deverá alterar o nível de log para Detalhado.  
  
 Para modificar os níveis de registro em log de diagnóstico para categorias de evento individuais:  
  
1.  Na Administração Central do SharePoint, clique em **Monitoramento**.  
  
2.  Clique em **Configurar log de diagnóstico**.  
  
3.  Role até **Serviço do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]**.  
  
4.  Expanda a categoria e selecione categorias individuais.  
  
     A**Solicitação de página de aplicativos** especifica eventos disparados pelo aplicativo de serviço ao localizar um [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] para carregar uma fonte de dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e comunicar-se com outros servidores no farm.  
  
     O**Processamento de solicitação** especifica eventos disparados por solicitações de consulta em relação a um banco de dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que é carregado em um servidor no farm.  
  
     O**Uso** especifica um evento relacionado à coleta de dados de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
5.  Em Evento menos crítico a ser relatado no log de eventos, selecione **Nenhum** para desabilitar o log de evento para a categoria, ou **Erro** para limitar o log para apenas erros.  
  
6.  Selecione **Detalhado** para registrar em log todos os eventos no log de eventos.  
  
7.  Em Evento menos crítico a ser relatado no log de rastreamento, selecione **Nenhum** para desabilitar o rastreamento para a categoria, ou **Erro** para limitar o rastreamento para apenas erros.  
  
8.  Selecione **Detalhado** para registrar em log todos os eventos no log de rastreamento.  
  
9. Clique em **OK**.  
  
##  <a name="bkmk_how2viewlogfiles"></a> Como exibir arquivos de log do SharePoint  
 Arquivos de log são arquivos de texto. Você pode abri-los em qualquer editor de texto. Você também pode usar aplicativos de visualizador de log de terceiros.  
  
#### <a name="use-a-text-editor"></a>Use o editor de textos  
 Se você estiver usando um editor de texto para solucionar problemas de erro de servidor do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , as dicas a seguir poderão ajudá-lo a localizar informações relevantes no arquivo:  
  
-   Para erros relacionados a publicação, exibição ou atualização de uma pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , pesquise no arquivo de log o nome da pasta de trabalho.  
  
-   Para erros que fornecem uma ID de correlação, copie a ID e use-a como um termo de pesquisa no arquivo de log.  
  
-   Procure status de erro "Alto" ou "Exceção." Pesquise por "Serviço do[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] ".  
  
-   Se você souber quando o erro ocorreu, use a data e as informações de tempo para restringir o escopo das entradas pelas quais você deve rolar.  
  
#### <a name="use-a-log-viewer-application"></a>Use um aplicativo de visualizador de log  
 Embora você possa usar um editor de texto para exibir os logs de rastreamento individualmente, um aplicativo de visualizador de log que permite exibir vários arquivos de log ao mesmo tempo pode ser muito mais útil. Felizmente, há vários aplicativos de visualizador de log de terceiros disponíveis para download no site da Codeplex que pode ajudar a exibir vários logs de rastreamento em um único espaço de trabalho.  
  
 As instruções a seguir incluem links para Visualizadores de Log populares de ULS do SharePoint que você pode baixar do Codeplex.  
  
1.  Vá para [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com) ou [Visualizador de log do ULS do SharePoint](http://go.microsoft.com/fwlink/?LinkId=150052) no site da Codeplex.  
  
2.  Clique na guia **Downloads** .  
  
3.  Clique no arquivo executável. Será **SharePointLogViewer.exe** ou **Visualizador de ULS 2.0 binário**.  
  
4.  Leia e aceite as condições de licenciamento.  
  
5.  Clique em **Salvar** para baixar o software para o sistema local.  
  
     Se você estiver baixando o Visualizador de Log do ULS do SharePoint, salve o ULSViewer.zip na pasta de Downloads.  
  
6.  Na pasta de Downloads, clique com o botão direito do mouse em ULSViewer.zip e selecione **Extrair Tudo**.  
  
7.  Especifique uma pasta de destino e clique em **Extrair**.  
  
8.  Na pasta que contém os arquivos de programa extraídos, clique duas vezes em **ULSViewer** e execute o aplicativo.  
  
9. Clique no ícone da pasta no canto superior esquerdo da janela do aplicativo.  
  
10. Navegue para C:\Arquivos de Programas\Common Files\Microsoft Shared\Extensões do Servidor da Web\14\Logs.  
  
11. Selecione um ou mais logs de rastreamento. Por padrão, os nomes de arquivos de log de rastreamento consistem no nome de computador mais informações de data e hora. O tipo de arquivo é Documento de Texto.  
  
12. Clique em **Abrir** e espere os arquivos carregarem.  
  
13. Use os filtros internos para selecionar os registros com base em severidade, processo, categoria ou um arquivo de texto definido pelo usuário. Você também pode clicar em títulos de coluna para alterar a ordem de classificação.  
  
#### <a name="entries-for-power-pivot-services"></a>Entradas para Serviços do Power Pivot  
 A tabela seguinte descreve entradas para operações de servidor do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] mais prováveis de serem localizadas em um arquivo de log do SharePoint.  
  
|Processar|Área|Categoria|Nível|Mensagem|Detalhes|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serviço|Uso|Detalhado|Não há nenhuma estatística de solicitação atual, nada para registrar em log.|A intervalos predefinidos, o serviço reporta estatísticas de resposta de consulta como um evento de uso para o sistema de coleta de dados de uso. Esta mensagem indica que não havia nenhuma estatística de consulta para reportar.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serviço|Front-end da Web|detalhado|Começando a localizar um servidor de aplicativos para fonte de dados =\<*caminho*>|Quando ele receber uma solicitação de conexão, o serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] identifica um [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] disponível para gerenciar a solicitação. Se houver somente um servidor no farm, o servidor local aceitará a solicitação em todos os casos.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serviço|Front-end da Web|Detalhado|Localizando o servidor de aplicativos bem-sucedido.|A solicitação foi alocada para um aplicativo de serviço do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serviço|Front-end da Web|detalhado|Solicitação de redirecionamento para o \< *origem do PowerPivotdata*> para o [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)].|A solicitação foi encaminhada para o [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)].|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serviço|Processamento de solicitação|detalhado|Solicitação de redirecionamento para UserName\<*usuário do SharePoint*> para o banco de dados|Uma conexão representada para a fonte de dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] foi criada em nome do usuário do SharePoint.|  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de dados de uso do PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)   
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  

