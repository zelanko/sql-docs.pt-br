---
title: "Identidade visual do portal da Web | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6dac97f7-02a6-4711-81a3-e850a6b40bf1
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# Identidade visual do portal da Web
Você pode alterar a aparência do portal da Web criando uma identidade visual para o seu negócio. Isso é feito por meio de um pacote de marca. O pacote de marca foi projetado para que você não precise de um conhecimento avançado de CSS (folha de estilo em cascata) para criá-lo.  
  
Neste tópico:  
  
-   [Criação do pacote de marca](#create)  
  
-   [Aplicação do pacote de marca ao portal da Web](#apply)  
  
-   [Exemplo de metadata.xml](#metadata)  
  
-   [Exemplo de colors.json](#colors)  
  
<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA?list=PLv2BtOtLblH3F--8WmK9QcLbx6dV_lVkL" frameborder="0" allowfullscreen></iframe>  
  
<a name="create">  
## Criação do pacote de marca  
  
Um pacote de marca para o Reporting Services é composto por três itens, e é empacotado como um arquivo zip.   
  
- color.json  
- metadata.xml  
- logo.png (opcional)  
  
Os arquivos devem ter os nomes listados acima. O arquivo zip pode receber o nome que você quiser.  
  
### metadata.xml  
  
O arquivo metadata.xml permite que você defina o nome do pacote de marca, e possui uma entrada de referência para os arquivos colors.json e logo.png.  
  
Para alterar o nome de seu pacote de marca, altere o atributo **name** do elemento **SystemResourcePackage**.  
  
    name="Multicolored example brand"  
  
Opcionalmente, você pode incluir uma imagem do logotipo em seu pacote de marca. Este item estaria listado dentro do elemento Contents.  
  
Exemplo sem um arquivo de logotipo.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
Exemplo com um arquivo de logotipo.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### Colors.json  
  
Quando o pacote de marca é carregado, o servidor extrai os pares de nome/valor apropriados do arquivo colors.json e os mescla com a folha de estilo LESS mestre, brand.less. Esse arquivo LESS é processado, e o arquivo CSS resultante é fornecido ao cliente. Todas as cores na folha de estilos seguem a representação hexadecimal de seis caracteres de uma cor.  
  
A folha de estilos LESS contém blocos que fazem referência a algumas variáveis LESS predefinidas, como as seguintes.  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
Embora isso se pareça com a sintaxe CSS, os valores de cor, prefixados com o símbolo @, são exclusivos ao LESS. Eles são variáveis cujos valores são definidos pelo arquivo json.  
  
Por exemplo, se o arquivo colors.json tiver os valores a seguir.  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
A saída processada procuraria a variável LESS **@primaryButtonBg** e veria que ela é mapeada para a propriedade json chamada **primary**, que neste exemplo é #009900. Portanto, geraria o CSS apropriado.  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
Todos os botões primários seriam processados na cor verde-escuro com texto em branco.  
  
O arquivo colors.json, para o Reporting Services, tem duas categorias principais nas quais os itens são agrupados.  
  
- **Interface**: inclui itens que são específicos ao portal da Web do Reporting Services.  
- **Tema**: inclui itens que são específicos aos relatórios móveis que você cria.  
  
A seção da interface é dividida nos seguintes agrupamentos.  
  
|Seção|Description|  
|---|---|  
|Primária|Cores do botão e da passagem do mouse.|  
|Secundário|Barra de título, barra de pesquisa, menu esquerdo (se for exibido) e cor do texto desses itens|  
|Principal neutro|Planos de fundo da Página inicial e da área de relatório.|  
|Neutro secundário|Planos de fundo das opções de pasta e caixa de texto, e o menu configurações.|  
|Terciário neutro|Planos de fundo de configurações do site.|  
|Mensagens de aviso/perigo/êxito|Cores para essas mensagens.|  
|KPI|Controla as cores para bom (1), neutro (0), neutro (-1) e nenhum.|  
  
Na primeira vez que você se conecta a um servidor com o Publicador de Relatório Móveis, que tem um pacote de marca implantado, o tema será adicionado aos temas disponíveis para uso no menu superior direito do aplicativo.  
  
![ssRSBrandingMobileReportPublisher](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
Assim, você pode usar esse tema para todos os relatórios móveis que criar, mesmo se eles não forem para o mesmo servidor no qual seu tema está implantado.   
  
### Como usar um logotipo  
  
Se você incluir um logotipo com o pacote de marca, ele será exibido no portal da Web no lugar do nome que você definiu para o portal da Web no menu Configurações do Site.  
  
O arquivo que você incluir para o logotipo deve usar o formato de arquivo PNG. As dimensões do arquivo serão ajustadas após o upload para o servidor. Ele deve ser dimensionado para 290px x 60px aproximadamente.  
  
<a name="apply">  
## Aplicação do pacote de marca ao portal da Web  
  
Para adicionar, baixar ou remover um pacote de marca, você pode fazer o seguinte.  
  
1.  Selecione a **engrenagem** no canto superior direito.  
  
2.  Selecione **Configurações de Site**.  
  
    ![ssRSGearMenu](../reporting-services/media/ssrsgearmenu.png)  
  
3.  Selecione **Identidade Visual**.  
  
    ![ssRSBranding](../reporting-services/media/ssrsbranding.png)  
  
**Pacote de marca instalado atualmente** exibirá o nome do pacote que foi carregado ou exibirá Nenhum.  
  
**Carregar pacote de marca** aplicará o pacote para o portal da Web. Você verá ele entrar em vigor imediatamente.  
  
Você também pode **Baixar** ou **Remover** o pacote. A remoção do pacote redefinirá imediatamente o portal da Web com a marca padrão.  
  
<a name="metadata">  
## Exemplo de metadata.xml  
  
    \<?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
  
<a name="colors">  
## Exemplo de Colors.json  
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  
  
  
  
  
  
  
  
  
  
