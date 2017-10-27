---
title: Usando o controle RSClientPrint em aplicativos personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 57312a2c4c75a9df1abc55baa833772c9949270c
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>Usando o controle RSClientPrint em aplicativos personalizados
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] controle ActiveX, **RSPrintClient**, fornece impressão do lado do cliente para relatórios exibidos no Visualizador de HTML. Ele fornece um **imprimir** caixa de diálogo para que um usuário pode iniciar um trabalho de impressão, visualizar um relatório, especificar páginas a serem impressas e alterar as margens. Durante uma operação de impressão do lado cliente, o servidor de relatório renderiza o relatório na extensão de renderização Image (EMF) e usa os recursos de impressão do sistema operacional para criar o trabalho de impressão e para enviá-lo para uma impressora.  
  
 A impressão do lado cliente oferece uma forma de controlar e de aprimorar a qualidade de uma cópia impressa de um relatório HTML ao esquivar-se das configurações de impressão do navegador do computador do usuário e usar as dimensões de página, as margens, o cabeçalho e o texto de rodapé do relatório para criar a saída de impressão. O controle de impressão lê valores de propriedade do relatório para definir o tamanho de página e as margens.  
  
 Os desenvolvedores que desejam habilitar o recurso de impressão do lado do cliente em barras de ferramentas de terceiros ou visualizadores podem acessar o controle ActiveX por meio de **RSClientPrint** objeto COM. O controle pode ser distribuído livremente. A lista a seguir oferece recomendações para o uso do controle:  
  
-   Use o controle para melhorar a impressão de relatórios baseados na Web. Você pode especificar o objeto em qualquer uma da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-compatível com linguagens de programação ou no script. O controle não foi criado para os aplicativos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms.  
  
-   Copie o arquivo .cab arquivo dos arquivos de programa do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e adicione-o à sua base de código de aplicativo personalizado.  
  
-   Use um \<objeto > marca para especificar o controle.  
  
-   Especifique uma URL relativa ou totalmente qualificada para o arquivo .cab no atributo OBJECT CODEBASE.  
  
-   Especifique as suas próprias informações de versão de aplicativo para o arquivo .cab para rastrear qual versão será usada em seu aplicativo.  
  
-   Examine os tópicos dos Manuais Online sobre a renderização de Image (EMF) para compreender como as páginas são renderizadas para a visualização de impressão e a saída.  
  
## <a name="rsprintclient-overview"></a>Visão geral de RSPrintClient  
 O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. O controle é empacotado como um arquivo CAB. O texto a **impressão** caixa de diálogo está localizada em todos os idiomas com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **RSPrintClient** controle ActiveX usa a extensão de renderização Image (EMF) para imprimir o relatório. As informações de dispositivo EMF a seguir são usadas: StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight e PageWidth. Outras configurações de informações de dispositivo para renderização de imagens não são suportadas.  
  
### <a name="language-support"></a>Suporte ao idioma  
 O controle de impressão fornece texto de interface do usuário em idiomas diferentes e aceita valores de entrada calibrados para diferentes sistemas de medidas. O sistema de medição e de idioma usado são determinados pelo **cultura** e **UICulture** propriedades. Ambas as propriedades aceitam valores LCID. Se você especificar um LCID para um idioma que seja uma variação de um idioma suportado, obterá o idioma correspondente mais próximo. Se você especificar um LCID que não seja suportado e para o qual não haja um LCID correspondente próximo, obterá o inglês (Estados Unidos).  
  
## <a name="using-rsclientprint-in-code"></a>Usando o RSClientPrint em código  
 O **RSClientPrint** objeto é usado para acessar programaticamente o controle ActiveX e seus métodos e propriedades. O controle fornece uma caixa de diálogo modal para a visualização de impressão.  
  
### <a name="specifying-default-values"></a>Especificando valores padrão  
 Você pode inicializar o **impressão** caixa de diálogo com os valores de margem e de página do relatório. Por padrão, o **impressão** caixa de diálogo é inicializada com valores da definição de relatório. Você pode usar os padrões ou especificar valores diferentes definindo as propriedades no objeto.  
  
 Todas as dimensões são definidas em milímetros. Conversão de medida ocorre em tempo de execução se o **cultura** e **UICulture** são definidas para localidades que não usam dimensões métricas.  
  
 Para entender quais valores são usados para dimensões de página e margens, você pode usar o **GetProperties** método para recuperar os valores padrão:  
  
-   **PageHeight** e **PageWidth** especificar a largura e altura de página padrão. Quando o controle de impressão é iniciado, esses valores de propriedade são usados para selecionar o tamanho de papel mais próximo disponível para a impressora atualmente selecionada. Se **PageWidth** for maior do que **PageHeight**, a orientação será definida como paisagem. Caso contrário, será definida como Retrato.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin**, e **BottomMargin** são definidas como 12,2 milímetros por padrão.  
  
 Essas propriedades são armazenadas no **Item** coleção de propriedades no servidor de relatório. Os valores serão substituídos sempre que uma definição de relatório for atualizada.  
  
### <a name="rsclientprint-properties"></a>Propriedades do RSClientPrint  
  
|Propriedade|Tipo|RW|Padrão|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|configuração de relatório|Obtém ou define a margem esquerda. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginRight|Double|RW|configuração de relatório|Obtém ou define a margem direita. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginTop|Double|RW|configuração de relatório|Obtém ou define a margem superior. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginBottom|Double|RW|configuração de relatório|Obtém ou define a margem inferior. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|PageWidth|Double|RW|configuração de relatório|Obtém ou define a largura da página. O valor padrão caso não seja definido pelo desenvolvedor ou a definição de relatório é 215.9 milímetros.|  
|PageHeight|Double|RW|configuração de relatório|Obtém ou define a altura da página. O valor padrão, caso não seja definido pelo desenvolvedor ou pela definição de relatório, é 279,4 milímetros.|  
|Cultura|Int32|RW|Localidade do navegador|Especifica o LCID (identificador de localidade). Este valor determina a unidade de medida para a entrada de usuário. Por exemplo, se um usuário digita **3**, o valor será medido em milímetros, se o idioma seja o francês ou em polegadas se o idioma for inglês (Estados Unidos). Os valores válidos incluem: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|UICulture|Cadeia de caracteres|RW|Cultura do cliente|Especifica localização da cadeia de caracteres da caixa de diálogo. O texto da caixa de diálogo Imprimir está localizado para estes idiomas: chinês simplificado, chinês tradicional, inglês, francês, alemão, italiano, japonês, coreano e espanhol. Os valores válidos incluem: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|Authenticate|Booliano|RW|Falso|Especifica se o controle emite um comando GET para o servidor de relatório para iniciar uma conexão de impressão fora de sessão.|  
  
### <a name="when-to-set-the-authenticate-property"></a>Quando definir a propriedade Authenticate  
 Quando você imprimir de uma sessão do navegador, você não precisa definir o **autenticar** propriedade. No contexto de uma sessão ativa, todas as solicitações do controle de impressão para o servidor de relatório serão manipuladas por meio do navegador. O navegador define as variáveis de sessão necessárias para a comunicação com o servidor de relatório.  
  
 Se você imprimir fora de sessão (por exemplo, enviar um relatório diretamente para uma impressora sem primeiro abri-lo), o controle de impressão deve emitir um HTTP **obter** solicitação para configurar a sessão com o servidor de relatório. Para emitir o **obter** solicitar, definir **autenticar** para **True**.  
  
 Você só precisará emitir a **obter** solicitação se você estiver usando o Windows integrados segurança ou a autenticação básica. Se você estiver usando autenticação de formulários, o **autenticar** propriedade será ignorada. O código do seu aplicativo precisa definir a sessão e autenticar o usuário usando a extensão de segurança personalizada fornecida por você. Se você estiver usando a autenticação de formulários, não se esqueça de definir o valor de expiração no cookie de autenticação como um valor que preserve sessões por um intervalo razoável. Se o valor for muito baixo, será solicitado que os usuários forneçam credenciais de logon sempre que o cookie expirar.  
  
### <a name="clsids"></a>CLSIDs  
 Quando você estiver executando o relatório nos locais, use os seguintes valores de CLSID.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Quando você estiver executando o relatório em Relatórios SQL do Windows Azure, use os seguintes valores de CLSID.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>Suporte de RSPrintClient para o método de impressão  
 O **RSClientPrint** objeto oferece suporte a **impressão** método usado para iniciar a caixa de diálogo de impressão. O **impressão** método tem os seguintes argumentos.  
  
|Argumento|E/S|Tipo|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|Entrada|Cadeia de caracteres|Especifica o diretório virtual do servidor de relatório (por exemplo, `https://adventure-works/reportserver`).|  
|ReportPathParameters|Entrada|Cadeia de caracteres|Especifica o nome completo para o relatório no namespace da pasta do servidor de relatório, incluindo os parâmetros. Os relatórios são recuperados por meio do acesso à URL. Por exemplo: "/AdventureWorks Sample Reports/Resumo de Vendas do Funcionário&EmpID=1234"|  
|ReportName|Entrada|Cadeia de caracteres|O nome curto do relatório (no exemplo anterior, o nome curto é Resumo de Vendas do Funcionário). Ele será exibido na caixa de diálogo Imprimir e na fila de impressão.|  
  
### <a name="example"></a>Exemplo  
 O exemplo HTML a seguir mostra como especificar o arquivo. cab, **impressão** método e as propriedades em JavaScript:  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>Consulte também  
 [Imprimir relatórios em um navegador com o controle de impressão &#40; Construtor de relatórios e SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Imprimir relatórios &#40; Construtor de relatórios e SSRS &#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Configurações de informações de dispositivo de imagem](../../../reporting-services/image-device-information-settings.md)  
  
  

