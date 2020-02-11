---
title: Configurar e exibir arquivos de log do SharePoint e log de diagnósticos (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 85f62d29-cdc6-45b3-be1f-ff1182939858
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f05edb30344b63781a89540ade8de4743bb715e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071851"
---
# <a name="configure-and-view-sharepoint-log-files--and-diagnostic-logging-powerpivot-for-sharepoint"></a>Configurar e exibir arquivos de log do SharePoint e log de diagnóstico (PowerPivot para SharePoint)
  
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são registrados em arquivos de log do SharePoint. Use as informações deste tópico para configurar informações de níveis de log e do arquivo de log de exibição. Você pode controlar quais eventos de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são registrados em log no arquivo. Você também pode controlar a severidade de mensagens que são registradas em log. Para obter mais informações, consulte [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Neste tópico:  
  
-   [Local do arquivo de log](#bkmk_filelocation)  
  
-   [Modificar níveis de log de diagnóstico para categorias de evento individuais](#bkmk_modifyloglevels)  
  
-   [Como exibir arquivos de log do SharePoint](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a>Local do arquivo de log  
 Por padrão, os arquivos de log do SharePoint são salvos no seguinte local:  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 A pasta LOGS contém arquivos de log (`.log`), arquivos de dados (`.txt`) e arquivos de uso (`.usage`). A convenção de nomenclatura de arquivo para um log de rastreamento do SharePoint é o nome de servidor seguido por um carimbo de data/hora. São criados logs de rastreamento de SharePoint em intervalos normais e sempre que há um IISRESET. É comum que haja muitos logs de rastreamento dentro de um período de 24 horas.  
  
##  <a name="bkmk_modifyloglevels"></a>Modificar níveis de log de diagnóstico para categorias de evento individuais  
 Por padrão, o log ULS dos eventos do PowerPivot é definido em *Meio*. Esta configuração é nova para o SQL Server 2012. Se você atualizou um servidor da versão anterior, o nível de log ainda poderia ser definido como *Detalhado*, o nível padrão no SQL Server 2008 R2. Se você estiver acostumado a revisar os logs ULS para obter informações de uso do servidor do PowerPivot, notará que, como resultado desta alteração, há menos informações sobre operações de servidor do PowerPivot.  
  
 Tirando as exceções, que são do tipo *Alta*, todas as mensagens de PowerPivot entram na categoria Detalhado. Se você quiser entradas de log para operações de servidor rotineiras como conexões, solicitações ou relatório de consulta, deverá alterar o nível de log para Detalhado.  
  
 Para modificar os níveis de registro em log de diagnóstico para categorias de evento individuais:  
  
1.  Na Administração Central do SharePoint, clique em **Monitoramento**.  
  
2.  Clique em **Configurar log de diagnóstico**.  
  
3.  Role até **Serviço PowerPivot**.  
  
4.  Expanda a categoria e selecione categorias individuais.  
  
     **Solicitação de página de aplicativo** Especifica eventos disparados pelo aplicativo de serviço ao [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] localizar um para carregar uma fonte de dados PowerPivot e se comunicar com outros servidores no farm.  
  
     O **processamento de solicitações** Especifica eventos disparados por solicitações de consulta em um banco de dados PowerPivot que é carregado em um servidor no farm.  
  
     O **uso** especifica um evento relacionado à coleta de dados de uso do PowerPivot.  
  
5.  Em Evento menos crítico a ser relatado no log de eventos, selecione **Nenhum** para desabilitar o log de evento para a categoria, ou **Erro** para limitar o log para apenas erros.  
  
6.  Selecione **Detalhado** para registrar em log todos os eventos no log de eventos.  
  
7.  Em Evento menos crítico a ser relatado no log de rastreamento, selecione **Nenhum** para desabilitar o rastreamento para a categoria, ou **Erro** para limitar o rastreamento para apenas erros.  
  
8.  Selecione **Detalhado** para registrar em log todos os eventos no log de rastreamento.  
  
9. Clique em **OK**.  
  
##  <a name="bkmk_how2viewlogfiles"></a>Como exibir arquivos de log do SharePoint  
 Arquivos de log são arquivos de texto. Você pode abri-los em qualquer editor de texto. Você também pode usar aplicativos de visualizador de log de terceiros.  
  
#### <a name="use-a-text-editor"></a>Use o editor de textos  
 Se você estiver usando um editor de texto para solucionar problemas de erro de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , as dicas a seguir poderão ajudá-lo a localizar informações relevantes no arquivo:  
  
-   Para erros relacionados a publicação, exibição ou atualização de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pesquise no arquivo de log o nome da pasta de trabalho.  
  
-   Para erros que fornecem uma ID de correlação, copie a ID e use-a como um termo de pesquisa no arquivo de log.  
  
-   Procure status de erro "Alto" ou "Exceção." Pesquise por "serviço PowerPivot".  
  
-   Se você souber quando o erro ocorreu, use a data e as informações de tempo para restringir o escopo das entradas pelas quais você deve rolar.  
  
#### <a name="use-a-log-viewer-application"></a>Use um aplicativo de visualizador de log  
 Embora você possa usar um editor de texto para exibir os logs de rastreamento individualmente, um aplicativo de visualizador de log que permite exibir vários arquivos de log ao mesmo tempo pode ser muito mais útil. Felizmente, há vários aplicativos de visualizador de log de terceiros disponíveis para download no site da Codeplex que pode ajudar a exibir vários logs de rastreamento em um único workspace.  
  
 As instruções a seguir incluem links para Visualizadores de Log populares de ULS do SharePoint que você pode baixar do Codeplex.  
  
1.  Vá para [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com) ou [Visualizador de log do ULS do SharePoint](https://go.microsoft.com/fwlink/?LinkId=150052) no site da Codeplex.  
  
2.  Clique na guia **downloads** .  
  
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
  
#### <a name="entries-for-powerpivot-services"></a>Entradas para serviços do PowerPivot  
 A tabela seguinte descreve entradas para operações de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] mais prováveis de serem localizadas em um arquivo de log do SharePoint.  
  
|Processo|Área|Categoria|Nível|Mensagem|Detalhes|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|Serviço PowerPivot|Uso|Verbose|Não há nenhuma estatística de solicitação atual, nada para registrar em log.|A intervalos predefinidos, o serviço reporta estatísticas de resposta de consulta como um evento de uso para o sistema de coleta de dados de uso. Esta mensagem indica que não havia nenhuma estatística de consulta para reportar.|  
|w3wp.exe|Serviço PowerPivot|Front-end da Web|Verbose|Começando a localizar um servidor de aplicativos para a fonte\<de dados =*caminho*>|Quando ele receber uma solicitação de conexão, o serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] identifica um [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] disponível para gerenciar a solicitação. Se houver somente um servidor no farm, o servidor local aceitará a solicitação em todos os casos.|  
|w3wp.exe|Serviço PowerPivot|Front-end da Web|Verbose|Localizando o servidor de aplicativos bem-sucedido.|A solicitação foi alocada para um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|w3wp.exe|Serviço PowerPivot|Front-end da Web|Verbose|Solicitação de redirecionamento para \<o> de *origem* do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]PowerPivotdata para o.|A solicitação foi encaminhada para o [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)].|  
|w3wp.exe|Serviço PowerPivot|Processamento de solicitação|Verbose|Solicitação de redirecionamento para\<*usuário do SharePoint*> para o banco de dados|Uma conexão representada para a fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] foi criada em nome do usuário do SharePoint.|  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de dados de uso do PowerPivot](power-pivot-usage-data-collection.md)   
 [Exibir e ler SQL Server arquivos de log da instalação](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
