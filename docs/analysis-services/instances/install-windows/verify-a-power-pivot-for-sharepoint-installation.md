---
title: Verifique se um PowerPivot para SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b715cf65001514acbd033800d6ae9807337c0ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="verify-a-power-pivot-for-sharepoint-installation"></a>Verifique uma Instalação do Power Pivot para SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Uma instância do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint instalada em um farm do SharePoint é administrada por meio da Administração Central do SharePoint. É possível, ao menos, verificar as páginas na Administração Central e nos sites do SharePoint para verificar a disponibilidade dos componentes e recursos do servidor [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . No entanto, para verificar integralmente uma instalação, você deve ter uma pasta de trabalho [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] que possa publicar no SharePoint e acessar em uma biblioteca. Para fins de teste, é possível publicar uma pasta de trabalho de exemplo que já contenha dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e usá-la para confirmar se essa integração com o SharePoint está configurada corretamente.  

  
##  <a name="verifyinstall"></a> Verificar a integração da Administração Central  
 Para verificar a integração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] com a Administração Central, faça o seguinte:  
  
1.  No menu Iniciar, clique em **Todos os Programas**, abra Produtos do Microsoft SharePoint 2016 ou e Produtos do Microsoft SharePoint 2013 e clique em **Administração Central do SharePoint 2016 ou Administração Central do SharePoint 2013**.  
  
2.  Digite seu nome de usuário e a senha e clique em **OK**.  
  
     Se desejar, você pode modificar as configurações do navegador para não ter que inserir um nome de usuário e uma senha vez que abrir a Administração Central. Para adicionar a Administração Central como um site confiável, faça o seguinte:  
  
    1.  No Internet Explorer, no menu Ferramentas, clique em **Opções da Internet**.  
  
    2.  Na guia Segurança, na seção **Selecionar uma zona para exibir ou alterar as configurações de segurança** , clique em Sites Confiáveis e em Sites.  
  
    3.  Desmarque a caixa de seleção **Exigir verificação do servidor (https) para todos os sites desta zona** .  
  
    4.  Em **Adicionar este site à zona**, digite a URL do site e clique em **Adicionar**.  
  
    5.  Clique em **Fechar**e em **OK**.  
  
        > [!NOTE]  
        >  A documentação de instalação do SharePoint inclui instruções adicionais para contornar erros de servidor proxy e para desabilitar a Configuração de Segurança Reforçada do Internet Explorer para que você possa baixar e instalar atualizações. Para obter mais informações, consulte a seção **Perform additional tasks** em [Deploy a single server with SQL Server](http://go.microsoft.com/fwlink/?LinkId=177754) no site da Microsoft.  
  
3.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar recursos de farm**.  
  
4.  Verifique se **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Recurso de Integração** está **Ativo**.  
  
5.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
6.  Verifique se o **Serviço de Sistema [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do SQL Server** foi iniciado.  
  
     Em um Farm do SharePoint com vários servidores, talvez seja necessário alterar o servidor que você está exibindo para validar que todos os servidores que você tenha implantado no [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] estejam em execução.  
  
7.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
8.  Clique em **Aplicativo de Serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Padrão** para abrir o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] desse aplicativo. No primeiro uso, o painel demora alguns minutos para carregar.  
  
     Como alternativa, clique no espaço vazio ao lado de **Aplicativo de Serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Padrão** para selecionar a linha e clique em **Propriedades** para exibir as configurações desse aplicativo de serviço. Você pode modificar os parâmetros de configuração e propriedades do aplicativo para alterar a configuração de seu servidor. Para obter mais informações sobre essas definições, veja [Criar e configurar um aplicativo de serviço do Power Pivot na Administração Central](../../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Verificar a integração no nível de site  
 Para verificar a integração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] com um site do SharePoint, faça o seguinte:  
  
1.  Em um navegador, abra o aplicativo Web criado. Se você usou valores padrão, você pode especificar http://\<o nome do computador > no endereço da URL.  
  
2.  Verifique se os recursos de acesso a dados e de processamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] estão disponíveis no aplicativo. É possível fazer isso verificando a presença de modelos de biblioteca fornecidos pelo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]:  
  
    1.  Selecione **Conteúdo do Site**.  
  
    2.  Na lista de aplicativos, você deverá ver **Biblioteca de Feeds de Dados** e **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]Galeria** do. Esses modelos de biblioteca são fornecidos pelo recurso do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , estando visíveis na lista Bibliotecas apenas se o recurso estiver integrado corretamente.  
  
## <a name="verify-data-access-on-the-server"></a>Verificar acesso a dados no servidor  
 Para verificar o acesso a dados [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no servidor, faça o seguinte:  
  
1.  [Baixe](http://go.microsoft.com/fwlink/?LinkID=219108) os exemplos de dados Picnic que acompanham um tutorial do Reporting Services. Você usará a pasta de trabalho de exemplo nesse download para verificar o acesso a dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Extraia os arquivos.  
  
2.  Carregue a pasta de trabalho (.xlsx) do Excel nos Documentos Compartilhados. A pasta de trabalho contém dados [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] inseridos.  
  
3.  Clique no documento para abri-lo na biblioteca.  
  
4.  Clique em uma segmentação de dados ou filtro no alto da pasta de trabalho. Mês, cor e tipo são segmentações de dados nesta pasta de trabalho. Clicar em uma segmentação de dados inicia uma consulta do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e comprova que seu servidor está funcionando. O servidor carregará dados [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em segundo plano e retornará os resultados.  
  
5.  Voltar para a biblioteca. Selecione a seta para baixo à direita da pasta de trabalho e clique em **Iniciar Power View**. Essa etapa confirma que o recurso do [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] no Reporting Services está funcionando. Se você não instalou o Reporting Services, ignore esta etapa.  
  
     Na próxima etapa, você se conectará ao servidor no Management Studio para verificar se os dados foram carregados e armazenados em cache.  
  
6.  Inicie o SQL Server Management Studio no grupo de programas [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] no menu Iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.  
  
7.  Em Tipo de Servidor, selecione **Analysis Services**.  
  
8.  Em nome do servidor, digite  **\<nome do servidor > \powerpivot**, onde  **\<nome do servidor >** é o nome do computador que tem o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint instalação.  
  
9. Clique em **Conectar**. Isso verifica se o servidor do Analysis Services está disponível.  
  
10. Em Pesquisador de Objetos, clique em **Bancos de Dados** para exibir a lista de arquivos de dados [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] carregados.  
  
11. No sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos estão armazenados no cache em disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivos, vá para a pasta [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]MSAS13.POWERPIVOT\OLAP\Backup\Sandboxes\Default [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Service Application. Cada banco de dados armazenado em cache é armazenado em sua própria pasta, usando uma convenção de nomenclatura baseada em GUID para assegurar um nome exclusivo.  
  
  
