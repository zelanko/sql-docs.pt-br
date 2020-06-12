---
title: Verificar uma instalação de PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5578bed4ce59ffb3c431c30e33418abe693a4165
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543838"
---
# <a name="verify-a-powerpivot-for-sharepoint-installation"></a>Verificar uma instalação do PowerPivot para SharePoint
  Uma instância do PowerPivot para SharePoint instalada em um farm do SharePoint é administrada por meio da Administração Central do SharePoint. É possível, ao menos, verificar as páginas na Administração Central e nos sites do SharePoint para verificar a disponibilidade dos componentes e recursos do servidor PowerPivot. No entanto, para verificar integralmente uma instalação, você deve ter uma pasta de trabalho PowerPivot que possa publicar no SharePoint e acessar em uma biblioteca. Para fins de teste, é possível publicar uma pasta de trabalho de exemplo que já contenha os dados PowerPivot e usá-la para confirmar se essa integração com o SharePoint está configurada corretamente.  
  
##  <a name="verify-central-administration-integration"></a><a name="verifyinstall"></a> Verificar a integração da Administração Central  
 Para verificar a integração do PowerPivot com a Administração Central, faça o seguinte:  
  
1.  No menu Iniciar, clique em **todos os programas**, abra produtos do Microsoft SharePoint 2010 e clique em **Administração Central do SharePoint 2010**.  
  
2.  Digite seu nome de usuário e a senha e clique em **OK**.  
  
     Se desejar, você pode modificar as configurações do navegador para não ter que inserir um nome de usuário e uma senha vez que abrir a Administração Central. Para adicionar a Administração Central como um site confiável, faça o seguinte:  
  
    1.  No Internet Explorer, no menu ferramentas, clique em **Opções da Internet**.  
  
    2.  Na guia Segurança, na seção **Selecionar uma zona para exibir ou alterar as configurações de segurança** , clique em Sites Confiáveis e em Sites.  
  
    3.  Desmarque a caixa de seleção **Exigir verificação do servidor (https) para todos os sites desta zona** .  
  
    4.  Em **Adicionar este site à zona**, digite a URL do site e clique em **Adicionar**.  
  
    5.  Clique em **Fechar**e clique em **OK**.  
  
        > [!NOTE]  
        >  A documentação de instalação do SharePoint inclui instruções adicionais para contornar erros de servidor proxy e para desabilitar a Configuração de Segurança Reforçada do Internet Explorer para que você possa baixar e instalar atualizações. Para obter mais informações, consulte a seção **Perform additional tasks** em [Deploy a single server with SQL Server](https://go.microsoft.com/fwlink/?LinkId=177754) no site da Microsoft.  
  
3.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar recursos de farm**.  
  
4.  Verifique se **Recurso de Integração com o PowerPivot** está **Ativo**.  
  
5.  Na administração central, em configurações do sistema, clique em **gerenciar serviços no servidor**.  
  
6.  Verifique se o **SQL Server Analysis Services** e o **Serviço de Sistema PowerPivot do SQL Server** foram iniciados.  
  
7.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
8.  Clique em **aplicativo de serviço PowerPivot padrão** para abrir o painel de gerenciamento PowerPivot para este aplicativo. No primeiro uso, o painel demora alguns minutos para carregar.  
  
     Como alternativa, clique no espaço vazio ao lado de **aplicativo de serviço PowerPivot padrão** para selecionar a linha e clique em **Propriedades** para exibir as definições de configuração para este aplicativo de serviço. Você pode modificar os parâmetros de configuração e propriedades do aplicativo para alterar a configuração de seu servidor. Para obter mais informações sobre essas configurações, consulte [criar e configurar um aplicativo de serviço PowerPivot na administração central](../../power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Verificar a integração no nível de site  
 Para verificar a integração do PowerPivot com um site do SharePoint, faça o seguinte:  
  
1.  Em um navegador, abra o aplicativo Web criado. Se você usou valores padrão, poderá especificar http:// \<your computer name> no endereço da URL.  
  
2.  Verifique se os recursos de acesso aos dados e de processamento do PowerPivot estão disponíveis no aplicativo. É possível fazer isso verificando a presença de modelos de biblioteca fornecidos pelo PowerPivot:  
  
    1.  Em ações do site, clique em **mais opções..**.  
  
    2.  Em bibliotecas, você deve ver **biblioteca de feeds de dados** e **Galeria PowerPivot**. Esses modelos de biblioteca são fornecidos pelo recurso do PowerPivot, estando visíveis na lista Bibliotecas apenas se o recurso estiver integrado corretamente.  
  
## <a name="verify-data-access-on-the-server"></a>Verificar acesso a dados no servidor  
 Para verificar o acesso a dados PowerPivot no servidor, faça o seguinte:  
  
1.  [Baixe](https://go.microsoft.com/fwlink/?LinkID=219108) os exemplos de dados Picnic que acompanham um tutorial do Reporting Services. Você usará a pasta de trabalho de exemplo nesse download para verificar o acesso aos dados PowerPivot. Extraia os arquivos.  
  
2.  Carregue a pasta de trabalho (.xlsx) do Excel nos Documentos Compartilhados. A pasta de trabalho contém dados PowerPivot inseridos.  
  
3.  Clique no documento para abri-lo na biblioteca.  
  
4.  Clique em uma segmentação de dados ou filtro no alto da pasta de trabalho. Mês, cor e tipo são segmentações de dados nesta pasta de trabalho. Clicar em uma segmentação de dados inicia uma consulta do PowerPivot e comprova que seu servidor está funcionando. O servidor carregará dados PowerPivot em segundo plano e retornará os resultados.  
  
5.  Voltar para a biblioteca. Selecione a seta para baixo à direita da pasta de trabalho e clique em **Iniciar Power View**. Essa etapa confirma que o recurso do [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] no Reporting Services está funcionando. Se você não instalou o Reporting Services, ignore esta etapa.  
  
     Na próxima etapa, você se conectará ao servidor no Management Studio para verificar se os dados foram carregados e armazenados em cache.  
  
6.  Inicie o SQL Server Management Studio no grupo de programas [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] no menu Iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.  
  
7.  Em tipo de servidor, selecione **Analysis Services**.  
  
8.  Em nome do servidor, digite ** \<server-name> \powerpivot**, em que **\<server-name>** é o nome do computador que tem a instalação do PowerPivot para SharePoint.  
  
9. Clique em **Conectar**. Isso verifica se o servidor do Analysis Services está disponível.  
  
10. No Pesquisador de objetos, você pode clicar em **bancos** de dados para exibir a lista de arquivos de dados PowerPivot que são carregados.  
  
11. No sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos estão armazenados no cache em disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivos, acesse \<drive> : \Program Files\Microsoft SQL Server\MSAS11. Pasta do aplicativo de serviço PowerPivot do POWERPIVOT\OLAP\Backup\Sandboxes\Default. Cada banco de dados armazenado em cache é armazenado em sua própria pasta, usando uma convenção de nomenclatura baseada em GUID para assegurar um nome exclusivo.  
  
  
