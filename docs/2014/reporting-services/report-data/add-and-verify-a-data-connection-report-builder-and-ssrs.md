---
title: Adicionar e verificar uma Conexão de dados ou uma fonte de dados (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 51ac8bee672064e07d66d924bc8efef0fc8aa1d5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946432"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>Adicionar e verificar uma conexão de dados ou uma fonte de dados (Construtor de Relatórios e SSRS)
  No Construtor de Relatórios, você pode adicionar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida no relatório. No Designer de Relatórios, você pode criar uma fonte de dados compartilhada ou uma fonte de dados inserida e implantá-la em um servidor de relatório.  
  
 Para adicionar uma fonte de dados compartilhada ao relatório, procure um servidor de relatório e selecione uma fonte de dados compartilhada. A fonte de dados compartilhada no seu relatório aponta para a definição de fonte de dados compartilhada no servidor de relatório.  
  
 Para criar uma fonte de dados inserida, você deve ter informações de conexão com a fonte de dados externa e deve saber quais permissões são necessárias para acessar os dados. Em geral, essas informações derivam do proprietário da fonte de dados. Você pode testar a conexão para verificar se as credenciais especificadas são suficientes.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md) e [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>Para criar uma referência a uma fonte de dados compartilhada  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Na caixa de texto **Nome** , digite um nome para a fonte de dados.  
  
    > [!NOTE]  
    >  Esse é o nome salvo na definição de relatório local. Esse nome não é o nome da fonte de dados compartilhada no servidor de relatório.  
  
3.  Selecione **Usar uma conexão compartilhada ou modelo de relatório**. A lista de fontes de dados compartilhadas e modelos de relatório usados recentemente é exibida. Para selecionar uma em um servidor de relatório, clique em **Procurar** e procure a pasta no servidor de relatório em que as fontes de dados compartilhadas estão disponíveis.  
  
4.  Selecione a fonte de dados compartilhada e clique em **Abrir**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 A fonte de dados será exibida no painel de dados do relatório.  
  
### <a name="to-create-an-embedded-data-source"></a>Para criar uma fonte de dados inserida  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Na caixa de texto **Nome** , digite um nome para a fonte de dados ou aceite o padrão.  
  
3.  Verifique se a opção **Usar uma conexão inserida em meu relatório** está marcada.  
  
    1.  Na lista suspensa **Selecionar o tipo de conexão** , selecione um tipo de fonte de dados; por exemplo, **Microsoft SQL Server** ou **OLE DB**.  
  
    2.  Especifique uma cadeia de conexão usando uma das alternativas a seguir:  
  
    -   Digite a cadeia de conexão diretamente na caixa de texto **Cadeia de conexão** . Para obter uma lista de exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
    -   Clique no botão de expressão (**fx)** para criar uma expressão que seja avaliada como uma cadeia de conexão. Na caixa de diálogo **Expressão** , digite a expressão no painel Expressão. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   Clique em **Criar** para abrir a caixa de diálogo **Propriedades de Conexão** para o tipo de fonte de dados escolhido na etapa 2.  
  
         Preencha os campos na caixa de diálogo **Propriedades de Conexão** , conforme adequado, para o tipo de fonte de dados. As propriedades de conexão incluem o tipo de fonte de dados, o nome da fonte de dados e as credenciais a serem usadas. Depois de especificar valores nesta caixa de diálogo, clique em **Testar Conexão** para verificar se a fonte de dados está disponível e se as credenciais especificadas estão corretas.  
  
4.  Clique em **Credenciais**.  
  
     Especifique as credenciais que serão usadas para essa fonte de dados. O proprietário da fonte de dados escolhe o tipo de credenciais com suporte. Em alguns casos, o proprietário da fonte de dados mantém uma fonte de dados compartilhada em um servidor de relatório e configura a fonte de dados com credenciais que você pode usar. Contate o proprietário da fonte de dados para obter essas informações. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 A fonte de dados será exibida no painel de dados do relatório.  
  
### <a name="to-verify-a-data-connection"></a>Para verificar uma conexão de dados  
  
1.  Na barra de ferramentas no painel de dados do relatório, clique duas vezes na fonte de dados. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Clique em **Testar Conexão**.  
  
3.  Se a conexão for bem-sucedida, a seguinte mensagem será exibida: "Conexão criada com êxito". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Se a conexão não for bem-sucedida, a seguinte mensagem será exibida: "Não é possível conectar-se à fonte de dados."  
  
5.  Clique em **Detalhes**e use as informações para corrigir o problema.  
  
     Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
