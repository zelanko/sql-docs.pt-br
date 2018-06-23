---
title: Usando o controle RSClientPrint em aplicativos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 30
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0c1f08f222fa1d902232373051e8d584b673ba5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122027"
---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>Usando o controle RSClientPrint em aplicativos personalizados
  O controle ActiveX [!INCLUDE[msCoName](../../../includes/msconame-md.md)], **RSPrintClient**, fornece impressão do lado do cliente para relatórios exibidos no Visualizador de HTML. Ele fornece uma caixa de diálogo **Imprimir** para que um usuário possa iniciar um trabalho de impressão, visualizar um relatório, especificar páginas a serem impressas e alterar as margens. Durante uma operação de impressão do lado cliente, o servidor de relatório renderiza o relatório na extensão de renderização Image (EMF) e usa os recursos de impressão do sistema operacional para criar o trabalho de impressão e para enviá-lo para uma impressora.  
  
 A impressão do lado cliente oferece uma forma de controlar e de aprimorar a qualidade de uma cópia impressa de um relatório HTML ao esquivar-se das configurações de impressão do navegador do computador do usuário e usar as dimensões de página, as margens, o cabeçalho e o texto de rodapé do relatório para criar a saída de impressão. O controle de impressão lê valores de propriedade do relatório para definir o tamanho de página e as margens.  
  
 Os desenvolvedores que desejam habilitar o recurso de impressão do lado do cliente em barras de ferramentas ou visualizadores de terceiros podem acessar o controle ActiveX por meio do objeto COM **RSClientPrint**. O controle pode ser distribuído livremente. A lista a seguir oferece recomendações para o uso do controle:  
  
-   Use o controle para melhorar a impressão de relatórios baseados na Web. Especifique o objeto em qualquer uma das linguagens de programação compatíveis com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ou em um script. O controle não foi criado para os aplicativos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms.  
  
-   Copie o arquivo .cab arquivo dos arquivos de programa do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e adicione-o à sua base de código de aplicativo personalizado.  
  
-   Use uma marcação \<OBJECT> para especificar o controle.  
  
-   Especifique uma URL relativa ou totalmente qualificada para o arquivo .cab no atributo OBJECT CODEBASE.  
  
-   Especifique as suas próprias informações de versão de aplicativo para o arquivo .cab para rastrear qual versão será usada em seu aplicativo.  
  
-   Examine os tópicos dos Manuais Online sobre a renderização de Image (EMF) para compreender como as páginas são renderizadas para a visualização de impressão e a saída.  
  
## <a name="rsprintclient-overview"></a>Visão geral de RSPrintClient  
 O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. O controle é empacotado como um arquivo CAB. O texto da caixa de diálogo **Imprimir** foi localizado para todos os idiomas com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O controle ActiveX **RSPrintClient** usa a extensão de renderização de Imagem (EMF) para imprimir o relatório. As informações de dispositivo EMF a seguir são usadas: StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight e PageWidth. Outras configurações de informações de dispositivo para renderização de imagens não são suportadas.  
  
### <a name="language-support"></a>Suporte ao idioma  
 O controle de impressão fornece texto de interface do usuário em idiomas diferentes e aceita valores de entrada calibrados para diferentes sistemas de medidas. O idioma e o sistema de medidas usados são determinados pelas propriedades **Culture** e **UICulture**. Ambas as propriedades aceitam valores LCID. Se você especificar um LCID para um idioma que seja uma variação de um idioma suportado, obterá o idioma correspondente mais próximo. Se você especificar um LCID que não seja suportado e para o qual não haja um LCID correspondente próximo, obterá o inglês (Estados Unidos).  
  
## <a name="using-rsclientprint-in-code"></a>Usando o RSClientPrint em código  
 O objeto **RSClientPrint** é usado para a obtenção de acesso de forma programática ao controle ActiveX e a seus métodos e propriedades. O controle fornece uma caixa de diálogo modal para a visualização de impressão.  
  
### <a name="specifying-default-values"></a>Especificando valores padrão  
 Inicialize a caixa de diálogo **Imprimir** com valores de margem e de página do relatório. Por padrão, a caixa de diálogo **Imprimir** é inicializada com valores obtidos na definição de relatório. Você pode usar os padrões ou especificar valores diferentes definindo as propriedades no objeto.  
  
 Todas as dimensões são definidas em milímetros. A conversão de medidas ocorrerá em tempo de execução se **Culture** e **UICulture** forem definidos com localidades que não usam medidas métricas.  
  
 Para entender quais valores são usados para as dimensões e margens de página, use o método **GetProperties** para recuperar os valores padrão:  
  
-   **PageHeight** e **PageWidth** especificam a altura e a largura de página padrão. Quando o controle de impressão é iniciado, esses valores de propriedade são usados para selecionar o tamanho de papel mais próximo disponível para a impressora atualmente selecionada. Se **PageWidth** for maior que **PageHeight**, a orientação será definida como Paisagem. Caso contrário, será definida como Retrato.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin** e **BottomMargin** são definidos como 12,2 milímetros por padrão.  
  
 Essas propriedades são armazenadas na coleção de propriedades **Item** no servidor de relatório. Os valores serão substituídos sempre que uma definição de relatório for atualizada.  
  
### <a name="rsclientprint-properties"></a>Propriedades do RSClientPrint  
  
|Propriedade|Tipo|RW|Padrão|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|configuração de relatório|Obtém ou define a margem esquerda. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginRight|Double|RW|configuração de relatório|Obtém ou define a margem direita. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginTop|Double|RW|configuração de relatório|Obtém ou define a margem superior. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|MarginBottom|Double|RW|configuração de relatório|Obtém ou define a margem inferior. O valor padrão, caso não seja definido pelo desenvolvedor ou especificado no relatório, é 12,2 milímetros.|  
|PageWidth|Double|RW|configuração de relatório|Obtém ou define a largura da página. O valor padrão, caso não seja definido pelo desenvolvedor ou pela definição de relatório, será 215,9 milímetros.|  
|PageHeight|Double|RW|configuração de relatório|Obtém ou define a altura da página. O valor padrão, caso não seja definido pelo desenvolvedor ou pela definição de relatório, é 279,4 milímetros.|  
|Cultura|Int32|RW|Localidade do navegador|Especifica o LCID (identificador de localidade). Este valor determina a unidade de medida para a entrada de usuário. Por exemplo, se um usuário digita `3`, o valor será medido em milímetros, se o idioma seja o francês ou em polegadas se o idioma for inglês (Estados Unidos). Os valores válidos incluem: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|UICulture|Cadeia de caracteres|RW|Cultura do cliente|Especifica localização da cadeia de caracteres da caixa de diálogo. O texto da caixa de diálogo Imprimir está localizado para estes idiomas: chinês simplificado, chinês tradicional, inglês, francês, alemão, italiano, japonês, coreano e espanhol. Os valores válidos incluem: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|Authenticate|Booliano|RW|Falso|Especifica se o controle emite um comando GET para o servidor de relatório para iniciar uma conexão de impressão fora de sessão.|  
  
### <a name="when-to-set-the-authenticate-property"></a>Quando definir a propriedade Authenticate  
 Quando você imprimir de uma sessão do navegador, não precisará definir a propriedade `Authenticate`. No contexto de uma sessão ativa, todas as solicitações do controle de impressão para o servidor de relatório serão manipuladas por meio do navegador. O navegador define as variáveis de sessão necessárias para a comunicação com o servidor de relatório.  
  
 Se você imprimir fora de sessão (por exemplo, o envio de um relatório diretamente para a impressora, sem que ele tenha sido aberto), o controle de impressão terá de emitir uma solicitação `GET` HTTP para configurar a sessão com o servidor de relatório. Para emitir a solicitação `GET`, defina `Authenticate` como `True`.  
  
 Você só precisará emitir a solicitação `GET` se estiver usando a segurança integrada do Windows ou a autenticação Básica. Se você estiver usando a autenticação de formulários, a propriedade `Authenticate` será ignorada. O código do seu aplicativo precisa definir a sessão e autenticar o usuário usando a extensão de segurança personalizada fornecida por você. Se você estiver usando a autenticação de formulários, não se esqueça de definir o valor de expiração no cookie de autenticação como um valor que preserve sessões por um intervalo razoável. Se o valor for muito baixo, será solicitado que os usuários forneçam credenciais de logon sempre que o cookie expirar.  
  
### <a name="clsids"></a>CLSIDs  
 Quando você estiver executando o relatório nos locais, use os seguintes valores de CLSID.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Quando você estiver executando o relatório em Relatórios SQL do Windows Azure, use os seguintes valores de CLSID.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>Suporte de RSPrintClient para o método de impressão  
 O objeto **RSClientPrint** dá suporte ao método **Print** usado para iniciar a caixa de diálogo Imprimir. O método **Print** tem os argumentos a seguir.  
  
|Argumento|E/S|Tipo|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|Entrada|Cadeia de caracteres|Especifica o diretório virtual do servidor de relatório (por exemplo, https://adventure-works/reportserver).|  
|ReportPathParameters|Entrada|Cadeia de caracteres|Especifica o nome completo para o relatório no namespace da pasta do servidor de relatório, incluindo os parâmetros. Os relatórios são recuperados por meio do acesso à URL. Por exemplo: "/AdventureWorks Sample Reports/Resumo de Vendas do Funcionário&EmpID=1234"|  
|ReportName|Entrada|Cadeia de caracteres|O nome curto do relatório (no exemplo anterior, o nome curto é Resumo de Vendas do Funcionário). Ele será exibido na caixa de diálogo Imprimir e na fila de impressão.|  
  
### <a name="example"></a>Exemplo  
 O exemplo de HTML a seguir mostra como especificar o arquivo .cab, o método **Print** e as propriedades em JavaScript:  
  
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
 [Imprimir relatórios em um navegador com o controle de impressão &#40;Construtor de Relatórios e SSRS&#41;](../../report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../report-builder/print-reports-report-builder-and-ssrs.md)   
 [Configurações de informações de dispositivo de imagem](../../image-device-information-settings.md)  
  
  