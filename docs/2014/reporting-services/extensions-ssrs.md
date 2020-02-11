---
title: Extensões
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 2e1f0dadca7a7bdb98f828ce33e617a0cce0e8cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413121"
---
# <a name="extensions-for-sql-server-reporting-services-ssrs"></a>Extensões para o SSRS (SQL Server Reporting Services)

  O servidor de relatório do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa extensões para modularizar os tipos de entrada ou de saída que aceita para autenticação, processamento de dados, renderização e entrega de relatórios. Isso facilita que instalações existentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utilizem novos padrões de software do setor, como um novo esquema de autenticação ou um tipo de fonte de dados personalizado. O servidor de relatório dá suporte aos seguintes tipos de extensões: autenticação personalizada, processamento de dados, processamento de relatórios, renderização e entrega, e as extensões que estão disponíveis para os usuários são configuráveis no arquivo de configuração RSReportServer.config. Por exemplo, você pode limitar os formatos de exportação que o visualizador de relatório tem permissão para usar. Um servidor de relatório requer pelo menos uma extensão de autenticação, de processamento de dados e de renderização. As extensões de entrega e de processamento de relatório são opcionais, mas necessárias se você desejar dar suporte aos controles de distribuição e personalização.  
  
 Este tópico descreve as extensões que estão prontamente disponíveis no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="security-extensions"></a>Extensões de Segurança

 São usadas extensões de segurança para autenticar e autorizar usuários e grupos em um servidor de relatório. A extensão de segurança padrão baseia-se na Autenticação do Windows. Também será possível criar uma extensão de segurança personalizada para substituir a segurança padrão se o modelo de implantação necessitar de uma abordagem de autenticação diferente (por exemplo, se você precisar de autenticação com base nos formulários para implantação na Internet ou extranet). Apenas uma extensão de segurança pode ser usada em uma única instalação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . É possível substituir a extensão de segurança padrão de Autenticação do Windows, contudo ela não pode ser utilizada ao lado de uma extensão de segurança personalizada.  
  
## <a name="data-processing-extensions"></a>Extensões de Processamento de Dados

 As extensões de Processamento de Dados são usadas para consultar uma fonte de dados e retornar um conjunto de linhas plano. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa diferentes extensões para interagir com tipos diferentes de fontes de dados. Você pode usar as extensões incluídas no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]ou desenvolver suas próprias extensões. Extensões de processamento de dados para fontes de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)], Hyperion Essbase, Teradata, OLE DB e ODBC são fornecidas. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também podem usar qualquer provedor de dados [!INCLUDE[vstecado](../includes/vstecado-md.md)] . A consulta de processo de extensões de processamento de dados solicita do componente Processador de Relatório, executando as seguintes tarefas:  
  
- Abrir uma conexão para uma fonte de dados.  
  
- Analisar uma consulta e retornar uma lista de nomes de campo.  
  
- Executar uma consulta na fonte de dados e retornar um conjunto de linhas.  
  
- Transmitir parâmetros a uma consulta, se necessário.  
  
- Iterar pelo conjunto de linhas e recuperar dados.  
  
Algumas extensões também podem executar as seguintes tarefas:  
  
- Analisar uma consulta e retornar uma lista dos nomes de parâmetros usados na consulta.  
  
- Analisar uma consulta e retornar a lista de campos usada para agrupamento.  
  
- Analisar uma consulta e retornar a lista de campos usada para classificação.  
  
- Fornecer um nome de usuário e senha para se conectar à fonte de dados.  
  
- Transmitir parâmetros com vários valores para uma consulta.  
  
- Iterar pelas linhas e recuperar metadados auxiliares.  
  
## <a name="rendering-extensions"></a>Extensões de Renderização

 As extensões de renderização transformam dados e informações de layout do Processador de Relatório em um formato específico ao dispositivo. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui sete extensões de renderização: HTML, Excel, CSV, XML, Imagem, PDF e [!INCLUDE[msCoName](../includes/msconame-md.md)] Word.  
  
- **Extensão de Renderização HTML** Quando você solicita um relatório de um servidor de relatório usando um navegador da Web, o servidor de relatório usa esta extensão de renderização para renderizar o relatório. A extensão de renderização HTML gera toda linguagem HTML usando a codificação UTF-8. Para obter mais informações, consulte [renderizando para HTML &#40;Construtor de relatórios e SSRS&#41;](report-builder/rendering-to-html-report-builder-and-ssrs.md) e [planejamento para Reporting Services e suporte ao navegador Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
- **Extensão de Renderização do Excel** A extensão de renderização do Excel renderiza relatórios que possam ser exibidos e modificados no [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 ou posterior. Esta extensão de renderização cria arquivos em BIFF (Formato de Arquivo de Intercâmbio Binário). BIFF é o formato de arquivo nativo para dados do Excel. Os relatórios renderizados no [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] dão suporte a todos os recursos disponíveis para qualquer planilha. Para obter mais informações, consulte [Exportar para Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
- **Extensão de Renderização CSV** A extensão de renderização CSV (Valor Separado por Vírgulas) renderiza relatórios em arquivos de texto não criptografado delimitados por vírgulas, sem nenhuma formatação. Os usuários podem abrir tais arquivos com um aplicativo de planilha, como o [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]ou com qualquer outro programa que leia arquivos de texto. Para obter mais informações, consulte [Exportar para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
- **Extensão de Renderização XML** A extensão de renderização XML renderiza relatórios em arquivos XML. Esses arquivos XML podem ser armazenados ou lidos por outros programas. Você também pode usar uma transformação XSLT para converter o relatório em outro esquema XML para ser usado por outro aplicativo. O XML gerado pela extensão de renderização XML é codificado como UTF-8. Para obter mais informações, consulte [Exportação para um XML &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-xml-report-builder-and-ssrs.md).  
  
-   **Extensão de Renderização de Imagem** A extensão de renderização de Imagem renderiza bitmaps ou metarquivos. A extensão pode renderizar relatórios nos seguintes formatos: BMP, EMF, GIF, JPEG, PNG, TIFF e WMF. Por padrão, a imagem é renderizada no formato TIFF, que pode ser exibido com o visualizador de imagem padrão do sistema operacional (por exemplo, Visualizador de Imagem e Fax do Windows). Você pode enviar a imagem para uma impressora a partir do visualizador. Usar a extensão de renderização de Imagem para renderizar relatórios garante que a aparência do relatório seja a mesma em todos os clientes. (Quando um usuário exibe um relatório em HTML, a aparência deste pode variar dependendo da versão ou das configurações do navegador do usuário, e das fontes disponíveis.) A extensão de renderização de Imagem renderiza o relatório no servidor, de modo que todos os usuários consultem a mesma imagem. Como o relatório é renderizado no servidor, todas as fontes usadas nele também devem estar instaladas no servidor. Para obter mais informações, consulte [Exportando para um arquivo de imagem &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md).  
  
- **Extensão de Renderização PDF** A extensão de renderização PDF renderiza relatórios em arquivos PDF que podem ser abertos e exibidos com o Adobe Acrobat 6.0 ou posterior. Para obter mais informações, consulte [Exportar para um arquivo PDF &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md).  
  
- **Extensão de Renderização do Word** A extensão de renderização do [!INCLUDE[msCoName](../includes/msconame-md.md)] Word renderiza um relatório como um documento do Word compatível com o [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 ou posterior. Para obter mais informações, consulte [Exportar para Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
## <a name="report-processing-extensions"></a>Extensões de Processamento de Relatório

 Podem ser adicionadas extensões de processamento de relatório a fim de prover processamento personalizado para itens de relatório que não estejam incluídos com [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Por padrão, um servidor de relatório pode processar tabelas, gráficos, matrizes, listas, caixas de texto, imagens e outros itens de relatório. Para adicionar recursos especiais a um relatório que necessita de processamento personalizado durante a execução do relatório (por exemplo, se você quiser inserir um mapa do [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint), crie uma extensão de processamento de relatório para tal.  
  
## <a name="delivery-extensions"></a>Extensões de Entrega

 O aplicativo de processamento em segundo plano usa extensões de entrega para entregar relatórios a vários locais. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email e uma extensão de entrega de compartilhamento de arquivos. A extensão de entrega de e-mail envia uma mensagem por meio do protocolo SMTP, quer o próprio relatório quer um link de URL para o relatório. Avisos curtos sem o vínculo de URL ou relatório também podem ser enviados a pagers, telefones ou outros dispositivos. A extensão de entrega de compartilhamento de arquivo salva os relatórios em uma pasta compartilhada na sua rede. É possível especificar o local, o formato da renderização, o nome do arquivo e as opções de substituição para o arquivo que você criar. A entrega de compartilhamento de arquivo pode ser usada para arquivar relatórios renderizados e como parte de uma estratégia para trabalhar com relatórios muito grandes. As extensões de entrega trabalham em conjunto com assinaturas. Quando um usuário cria uma assinatura, ele escolhe uma das extensões de entrega disponíveis para determinar como o relatório será entregue.