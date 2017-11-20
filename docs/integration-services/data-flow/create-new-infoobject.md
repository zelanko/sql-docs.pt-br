---
title: Criar novo InfoObject | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3587a633-1c0b-4d63-a22a-6b2b93923c3a
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0135f5cbbe81cbe8d4a8c530a1d63c84a27f7d2
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="create-new-infoobject"></a>Criar Novo InfoObject
  Use a caixa de diálogo **Criar Novo InfoObject** para criar um novo InfoObject no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoObject** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, confira [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar Novo InfoObject**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa do grupo **Criar Objetos SAP BW** , execute uma destas etapas para criar um InfoObject:  
  
    1.  Para criar um InfoObject diretamente, selecione **InfoObject**e clique em **Criar** para abrir a caixa de diálogo **Criar Novo InfoObject** .  
  
    2.  Para criar um InfoObject ao criar um InfoCube, selecione **InfoCube**e clique em **Criar**. Na caixa de diálogo **Criar InfoCube para os Dados da Transação** , na coluna **IObject** de uma das linhas na lista, selecione **Criar** para abrir a caixa de diálogo **Criar Novo InfoObject** .  
  
        > [!NOTE]  
        >  Cada linha na tabela representa uma coluna no fluxo de dados do pacote.  
  
    3.  Para criar um InfoObject ao criar um InfoSource para dados transacionais, selecione **InfoSource**e clique em **Criar**. Na caixa de diálogo **Criar InfoSource** , selecione **Dados da Transação**e clique em **OK**. Na caixa de diálogo **Criar InfoSource para os Dados da Transação** , na coluna **IObject** de uma das linhas na lista, selecione **Criar** para abrir a caixa de diálogo **Criar Novo InfoObject** .  
  
        > [!NOTE]  
        >  Cada linha na tabela representa uma coluna no fluxo de dados do pacote.  
  
    4.  Para criar um InfoObject ao criar um InfoSource para dados mestres, selecione **InfoSource**e clique em **Criar**. Na caixa de diálogo **Criar InfoSource** , selecione **Dados Mestres**e clique em **OK**. Na caixa de diálogo **Criar InfoSource para Dados Mestres** , clique em **Novo** para abrir a caixa de diálogo **Criar Novo InfoObject** .  
  
 Você também pode abrir a caixa de diálogo **Criar Novo InfoObject** clicando em **Novo** na seção **Atributos** da caixa de diálogo **Criar Novo InfoObject** .  
  
## <a name="general-options"></a>Opções gerais  
 **Característica**  
 Crie um InfoObject que representa os dados da dimensão.  
  
 **Valor-chave**  
 Crie um InfoObject que representa os dados de fato.  
  
 **Nome do InfoObject**  
 Digite um nome para o InfoObject.  
  
 **Descrição breve**  
 Insira uma descrição curta para o InfoObject.  
  
 **Descrição longa**  
 Insira uma descrição longa para o InfoObject.  
  
 **Com dados mestres**  
 Indica que o InfoObject contém dados mestres na forma de atributos, textos ou hierarquias.  
  
> [!NOTE]  
>  Selecione esta opção se o InfoObject representar dados dimensionais e você tiver selecionado a opção **Característica** .  
  
 **Permitir caracteres minúsculos**  
 Permitir caracteres minúsculos nos dados do InfoObject.  
  
 **Salvar e ativar**  
 Salvar e ativar o novo InfoObject.  
  
## <a name="data-type-options"></a>Opções de tipo de dados  
 **CHAR - Cadeia de caracteres**  
 Indica que o InfoObject contém dados de caracteres.  
  
 **NUMC - Cadeia de Caracteres Numéricos**  
 Indica que o InfoObject contém dados numéricos.  
  
 **DATS - Data (AAAAMMDD)**  
 Indica que o InfoObject contém dados de data.  
  
 **TIMS - Hora (HHMMSS)**  
 Indica que o InfoObject contém dados de hora.  
  
 **Comprimento**  
 Insira o comprimento dos dados.  
  
## <a name="text-options"></a>Opções de texto  
 **Com textos**  
 Indica que o InfoObject contém textos.  
  
 **Texto curto**  
 Indica que o InfoObject contém textos curtos.  
  
 **Texto médio**  
 Indica que o InfoObject contém textos médios.  
  
 **Texto longo**  
 Indica que o InfoObject contém textos longos.  
  
 **Dependente do idioma do texto**  
 Indica que os textos dependem da linguagem.  
  
 **Dependente da hora do texto**  
 Indica que os textos dependem da hora.  
  
## <a name="attributes-section"></a>Seção de atributos  
 A seção **Atributos** consiste em uma lista de atributos para o InfoObject e as opções que permitem adicionar e remover atributos da lista.  
  
### <a name="attributes-list"></a>Lista de atributos  
 A lista **Atributos** exibe os atributos do InfoObject que você está criando. A lista **Atributos** tem os seguintes cabeçalhos de coluna:  
  
 **InfoObject**  
 Exiba o nome do InfoObject.  
  
 **Description**  
 Visualize a descrição do InfoObject.  
  
 **Tipo do InfoObject**  
 Exiba o tipo do InfoObject. A tabela a seguir lista os valores possíveis do tipo.  
  
|Value|Description|  
|-----------|-----------------|  
|CHA|Características|  
|KYF|Valores-chave|  
|UNI|Unidades|  
|TIM|Características de hora|  
  
### <a name="attributes-options"></a>Opções do atributo  
 Use as opções a seguir para adicionar e remover atributos para o InfoObject que você está criando:  
  
 **Adicionar**  
 Adicione um InfoObject existente como um atributo.  
  
 Para adicionar um InfoObject existente, clique em Adicionar e use a caixa de diálogo **Pesquisar InfoObject** para localizar o InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 **Novo**  
 Adicione um novo InfoObject como um atributo.  
  
 Para criar e adicionar um novo InfoObject, clique em Novo e use uma nova instância da caixa de diálogo **Criar Novo InfoObject** para criar o novo InfoObject.  
  
 **Remover**  
 Remova o InfoObject selecionado da lista **Atributos** .  
  
## <a name="see-also"></a>Consulte também  
 [Criar InfoCube para os dados da transação](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [Criar InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Criar InfoSource para dados de transação](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [Criar InfoSource para dados mestres](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Ajuda F1 do Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

