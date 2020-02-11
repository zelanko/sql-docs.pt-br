---
title: Página Propriedades de fontes de dados (Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f37edda0-19e6-489e-b544-8751fa6b6cfb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e094c61fe26faca4e60303c340f2b3557c0f148e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109417"
---
# <a name="data-sources-properties-page-report-manager"></a>Página Propriedades de Fontes de Dados (Gerenciador de Relatórios)
  Use a página de propriedades de Fontes de Dados para definir como o relatório atual se conecta a uma fonte de dados externa. Você pode substituir as informações de conexão de fonte de dados publicadas originalmente com o relatório. Se várias fontes de dados forem usadas em um relatório, cada fonte de dados terá sua própria seção na página de propriedades. As fontes de dados são listadas na ordem em que foram definidas no relatório.  
  
 Ao especificar uma fonte de dados para usar com o relatório, você pode usar uma fonte de dados compartilhada que é criada e gerenciada separadamente dos relatórios que usa. Se você não quiser usar um item de fonte de dados compartilhada, poderá definir uma conexão de fonte de dados para usar com o relatório.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-data-sources-properties-page"></a>Para abrir a página de propriedades de Fontes de Dados  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório para o qual você deseja selecionar uma fonte de dados.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Isso abre a página de propriedades **geral** do relatório.  
  
4.  Selecione a guia **Fontes de Dados** .  
  
## <a name="options"></a>Opções  
 **Uma fonte de dados compartilhada**  
 Especifique uma fonte de dados compartilhada a ser usada com o relatório. Para obter mais informações sobre como criar uma nova fonte de dados, consulte [criar, excluir ou modificar uma fonte de dados compartilhada &#40;Report Manager&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Procurar**  
 Clique em **Procurar** para abrir a página Seleção de Fonte de Dados usada para selecionar uma fonte de dados compartilhada. Para obter mais informações, consulte [página de seleção de fonte de dados &#40;Report Manager&#41;](../../2014/reporting-services/data-source-selection-page-report-manager.md).  
  
 **Uma fonte de dados personalizada**  
 Especifique como o relatório se conecta à fonte de dados.  
  
 As opções a seguir são usadas para especificar uma conexão de fonte de dados personalizada.  
  
 **Tipo de fonte de dados**  
 Especifique a extensão de processamento de dados usada para processar dados da fonte de dados. Para obter a lista de extensões de dados internas, consulte [fontes de dados com suporte pelo Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md). Extensões de processamento de dados adicionais podem estar disponíveis em fornecedores de terceiros.  
  
 **Cadeia de conexão**  
 Especifique a cadeia de conexão que o servidor de relatório utiliza para conectar-se à fonte de dados. O tipo de conexão determina a sintaxe que você deve usar. Por exemplo, uma cadeia de caracteres de conexão da extensão do processamento de dados XML é uma URL para um documento XML. Na maioria dos casos, uma cadeia de caracteres de conexão típica especifica o servidor de banco de dados e um arquivo de dados. O exemplo a seguir ilustra uma cadeia de conexão usada para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] chamado MyData:  
  
 `data source=<a SQL Server instance>;initial catalog=MyData`  
  
 Uma cadeia de conexão pode ser configurada como uma expressão para que você possa especificar a fonte de dados em tempo de execução. Expressões de fonte de dados são definidas no relatório, no Designer de Relatórios. Expressões de fonte de dados não podem ser definidas, exibidas ou modificadas no Gerenciador de Relatórios. Porém, você pode substituir uma expressão de fonte de dados clicando em **Substituir Padrão** para digitar uma cadeia de conexão estática. Se você quiser retornar à expressão, clique em **Reverter em Padrão**. O servidor de relatórios armazena a cadeia de caracteres de conexão original no caso de você precisar restaurá-la. Para usar expressões de fonte de dados, você deve usar as informações de conexão de fonte de dados publicadas originalmente no relatório. As fontes de dados compartilhadas não dão suporte ao uso de expressões na cadeia de conexão.  
  
 **Conectar usando**  
 Especifica opções que determinam como as credenciais são obtidas.  
  
> [!IMPORTANT]  
>  Se forem fornecidas credenciais na cadeia de conexão, serão ignorados as opções e os valores fornecidos nesta seção. Observe que, se você especificar as credenciais na cadeia de conexão, os valores serão exibidos em texto não criptografado para todos os usuários que exibirem essa página.  
  
 **Credenciais fornecidas pelo usuário que está executando o relatório**  
 Cada usuário deve digitar um nome de usuário e uma senha para acessar a fonte de dados. Você pode definir o texto do prompt que solicita as credenciais do usuário. A cadeia de caracteres de texto padrão é "Digite um nome de usuário e uma senha para acessar a fonte de dados".  
  
 Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados** se as credenciais que o usuário fornecer forem credenciais de Autenticação do Windows. Não marque esta caixa de seleção se você estiver usando autenticação de banco de dados (por exemplo, Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ).  
  
 **Credenciais armazenadas com segurança no servidor de relatórios**  
 Armazene um nome de usuário criptografado e a senha no banco de dados do servidor de relatórios. Selecione essa opção para executar um relatório autônomo (por exemplo, relatórios iniciados por agendas ou eventos em vez de pela ação do usuário). Se você estiver usando segurança padrão, o nome de usuário deve ser uma conta de domínio do Windows. Especifique a conta neste formato: \<domínio>\\<nome de\>usuário. A conta especificada deve ter permissões locais de logon no computador que hospeda a fonte de dados usada pelo relatório.  
  
 Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados** se as credenciais forem credenciais de Autenticação do Windows. Não marque esta caixa de seleção se você estiver usando autenticação de banco de dados (por exemplo, Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ).  
  
 Selecione **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados** para permitir delegação de credenciais de banco de dados, mas somente se uma fonte de dados oferecer suporte a representação. No caso de bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , essa opção define a função SETUSER.  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]dá suporte apenas a credenciais de conta do Windows. Portanto, selecione ambas as opções "Usar as credenciais do Windows ao conectar-se à fonte de dados" e "Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados" para uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Segurança integrada do Windows**  
 Use as credenciais do Windows do usuário atual para acessar a fonte de dados. Selecione essa opção quando as credenciais usadas para acessar a fonte de dados forem as mesmas que as usadas para fazer logon no domínio de rede. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se Kerberos não estiver habilitado, as credenciais do Windows poderão ser passadas para outro computador. Se forem necessárias conexões de computador adicionais, ocorrerá um erro em vez da exibição dos dados esperados.  
  
 Um administrador de servidor de relatórios pode desabilitar o uso da segurança integrada do Windows para acessar fontes de dados de relatório. Se esse valor estiver esmaecido, o recurso não estará disponível.  
  
 Não use essa opção se você planeja programar ou assinar a esse relatório. Processamento de relatório programado ou autônomo requer credenciais que podem ser obtidas sem entrada de usuário ou contexto de segurança de um usuário atual. Somente credenciais armazenadas fornecem esse recurso. Por esse motivo, o servidor de relatórios evita que você agende relatório ou processe assinatura, se o relatório estiver configurado para tipo de credencial de segurança integrada do Windows. Se você escolher essa opção para um relatório já assinado ou com operações agendadas, as operações de assinatura e agendamento serão interrompidas.  
  
 **Não são necessárias credenciais**  
 Especifique que não são necessárias credenciais para acessar a fonte de dados. Observe que se uma fonte de dados necessitar de um logon de usuário, a escolha dessa opção não terá nenhum efeito. Você só deve escolher esta opção se a conexão de fonte de dados não requerer credenciais de usuário.  
  
 Para usar essa opção, a conta de execução autônoma deve estar previamente configurada para sua implantação de servidor de relatórios. A conta de execução autônoma é usada para conectar a fontes externas, quando outras fontes de credenciais não estiverem disponíveis. Se você especificar essa opção e a conta não estiver configurada, a conexão com a fonte de dados do relatório falhará e o processamento do relatório não ocorrerá.  Para obter mais informações sobre essa conta, consulte [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar fontes de dados de relatório](report-data/manage-report-data-sources.md)   
 [Especificar informações de credencial e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
