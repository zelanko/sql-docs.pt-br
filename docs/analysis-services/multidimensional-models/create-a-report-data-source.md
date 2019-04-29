---
title: Criar uma fonte de dados de relatório | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b6e811f9114a484f7b0b68ca9782b9b60e366383
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866876"
---
# <a name="create-a-report-data-source"></a>Criar uma fonte de dados de relatório
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para que o Power View se conecte a um modelo multidimensional, você deve criar uma definição de fonte de dados de relatório compartilhada, também conhecida como um arquivo .rsds, em uma biblioteca do SharePoint. O arquivo .rsds especifica o nome de uma instância de servidor do Analysis Services, um tipo de conexão, uma cadeia de conexão, além de credenciais usadas para se conectar ao modelo multidimensional. Quando um usuário clica no .rsds, um novo relatório em branco do Power View (um arquivo .rdlx) é aberto no navegador.  
  
 Para criar uma conexão .rsds, você deve ter o SQL Server 2012 (ou posterior) Reporting Services e o suplemento Reporting Services para SharePoint 2010 ou SharePoint 2013 instalado.  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>Criar uma conexão de Fonte de Dados de Relatório (.rsds) para um modelo multidimensional  
 Antes de começar, você precisa saber:  
  
-   O nome da instância de servidor do Analysis Services em execução no modo Multidimensional.  
  
-   O nome do banco de dados multidimensional ao qual deseja se conectar.  
  
-   O nome do cubo, se houver mais de um.  
  
-   (Opcional) Nome da perspectiva.  
  
-   (Opcional) Identificador de localidade.  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>Para criar um arquivo de Fonte de Dados de Relatório compartilhada (.rsds) (SharePoint 2010)  
  
1.  Clique na guia **Documentos** na faixa de opções da biblioteca.  
  
2.  Clique em **Novo Documento** > **Fonte de Dados de Relatório**.  
  
    > [!NOTE]  
    >  Caso você não veja o item **Fonte de Dados de Relatório** no menu, isso significa que o tipo de conteúdo da fonte de dados de relatório não foi habilitado para essa biblioteca. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  Na página **Propriedades da Fonte de Dados** , em **Nome**, digite um nome para o arquivo .rsds de conexão.  
  
4.  Em **Tipo de Fonte de Dados**, selecione **Modelo Semântico de BI da Microsoft para Power View**.  
  
5.  Em **Cadeia de Conexão**, especifique o nome do servidor do Analysis Services, o nome do banco de dados, o nome do cubo e todas as configurações opcionais.  
  
     Cadeia de conexão: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'`  
  
    > [!NOTE]  
    >  Se houver mais de um cubo, você deve especificar um nome de cubo.  
  
     (Opcional) Os cubos podem ter perspectivas que fornecem aos usuários uma exibição de seleção em que apenas determinadas dimensões e/ou grupos de medidas ficam visíveis no cliente. Para especificar uma perspectiva, insira o nome da perspectiva como um valor para a propriedade Cubo: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>'`  
  
     (Opcional) Os cubos podem ter traduções de dados e metadados especificadas para diversos idiomas no modelo. Para ver as traduções (dados e metadados), você precisará adicionar a propriedade "Identificador de localidade" à cadeia de conexão: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'; Locale Identifier=<identifier number>`  
  
6.  Em **Credenciais**, especifique como o servidor de relatório obtém credenciais para acessar a fonte de dados externa.  
  
    -   Selecione **Autenticação do Windows (integrada)** se desejar acessar os dados usando as credenciais do usuário que abriu o relatório. Não selecione essa opção se o site ou farm do SharePoint utilizar autenticação de formulários ou se conectar com o servidor de relatório usando uma conta confiável. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se a autenticação Kerberos não estiver habilitada, as credenciais do Windows poderão ser passadas apenas para outro computador. Isso significa que, se a fonte de dados externa estiver em outro computador, exigindo uma conexão adicional, você receberá uma mensagem de erro em vez dos dados esperados.  
  
    -   Selecione **Prompt para credenciais** se quiser que o usuário insira suas credenciais sempre que executar o relatório. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório.  
  
    -   Selecione **Credenciais armazenadas** se quiser acessar os dados usando um único conjunto de credenciais. As credenciais são criptografadas antes de serem armazenadas. Você pode selecionar opções que determinam como as credenciais armazenadas são autenticadas. Selecione Usar como credenciais do Windows se as credenciais armazenadas pertencerem a uma conta de usuário do Windows. Selecione **Definir o contexto de execução para esta conta** se desejar definir o contexto de execução no servidor de banco de dados.  
  
    -   Selecione **Não são necessárias credenciais** se especificar credenciais na cadeia de conexão ou se desejar executar o relatório usando uma conta de privilégios mínimos.  
  
7.  Clique em **Testar Conexão** para validar.  
  
8.  Selecione **Habilitar esta fonte de dados** se desejar que a fonte de dados esteja ativa. Se a fonte de dados estiver configurada mas não ativa, os usuários receberão uma mensagem de erro quando tentarem criar um relatório.  
  
  
