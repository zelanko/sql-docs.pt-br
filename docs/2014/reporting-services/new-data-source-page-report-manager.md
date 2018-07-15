---
title: Nova fonte de dados página (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 57c22c0f39b411510fb70c5a5068ce4930674555
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280382"
---
# <a name="new-data-source-page-report-manager"></a>Página Nova Fonte de Dados (Gerenciador de Relatórios)
  Use a página Nova Fonte de Dados para criar um item fonte de dados compartilhada. Uma fonte de dados compartilhada define uma conexão com uma fonte de dados externa. Com uma fonte de dados compartilhada, você pode criar e manter as configurações de conexão da fonte de dados separadas dos relatórios, modelos e assinaturas controladas por dados que usam a fonte de dados.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-new-data-source-page"></a>Para abrir a página Nova Fonte de Dados  
  
1.  Abra o Gerenciador de Relatórios e navegue até a pasta na qual você deseja criar uma fonte de dados.  
  
2.  Na barra de ferramentas, clique em **Nova Fonte de Dados**. Você deve ter permissões de Gerenciador de Conteúdo para criar uma fonte de dados compartilhada.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome para a fonte de dados compartilhada, que é usado para identificar o item na hierarquia de pastas do servidor de relatórios.  
  
 **Descrição**  
 Fornece informações sobre a fonte de dados compartilhada. Essa descrição é exibida na página Conteúdo.  
  
 **Ocultar na exibição de lista**  
 Selecione essa opção para ocultar a fonte de dados compartilhada de usuários que estão usando o modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando se navega na hierarquia de pastas do servidor de relatórios. Na exibição de lista, os nomes de itens e as descrições fluem pela página. O formato alternativo é o modo de exibição de detalhes. A exibição de detalhes omite descrições, mas contém outras informações sobre o item. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Para restringir o acesso a um item, você deverá criar uma atribuição de função  
  
 **Habilitar esta fonte de dados**  
 Selecione para habilitar ou desabilitar a fonte de dados compartilhada. Você pode desabilitar a fonte de dados compartilhada para evitar o processamento de todos os relatórios e modelos que referenciam o item.  
  
 **Tipo de fonte de dados**  
 Especifique a extensão de processamento de dados usada para processar dados da fonte de dados. Servidor de relatórios inclui extensões de processamento de dados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], SAP, XML, ODBC e OLE DB. Extensões de processamento de dados adicionais podem estar disponíveis em fornecedores de terceiros.  
  
 Para obter mais informações sobre o suporte de fonte de dados remota e não-SQL, consulte [recursos compatíveis com as edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (HYPERLINK "http://go.microsoft.com/fwlink/?linkid=232473" http://go.microsoft.com/fwlink/?linkid=232473) e [dados de fontes com suporte pela emissão de relatórios Serviços &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 **Cadeia de conexão**  
 Especifique a cadeia de conexão que o servidor de relatório utiliza para conectar-se à fonte de dados. O tipo de conexão determina a sintaxe que você deve usar. Por exemplo, uma cadeia de caracteres de conexão da extensão do processamento de dados XML é uma URL para um documento XML. Na maioria dos casos, uma cadeia de caracteres de conexão típica especifica o servidor de banco de dados e um arquivo de dados.  
  
 O exemplo a seguir ilustra uma cadeia de caracteres de conexão usada para conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] banco de dados:  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 Para obter mais informações sobre diferentes maneiras de especificar uma cadeia de caracteres de conexão e exemplos, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 **Conecte-se usando**  
 Especifique opções que determinam como as credenciais são obtidas.  
  
> [!IMPORTANT]  
>  Se forem fornecidas credenciais na cadeia de conexão, serão ignorados as opções e os valores fornecidos nesta seção. Observe que, se você especificar as credenciais na cadeia de conexão, os valores serão exibidos em texto não criptografado para todos os usuários que exibirem essa página.  
  
 **Credenciais fornecidas pelo usuário que executa o relatório (conectar usando)**  
 Cada usuário é solicitado a digitar um nome de usuário e senha para acessar a fonte de dados. Você pode definir o texto do prompt que solicita as credenciais do usuário. A cadeia de caracteres de texto padrão é "Digite um nome de usuário e uma senha para acessar a fonte de dados".  
  
 Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados** se as credenciais que o usuário fornecer forem credenciais de Autenticação do Windows. Não selecione essa caixa de seleção se você estiver usando a autenticação de banco de dados (por exemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação).  
  
 **Credenciais armazenadas com segurança no servidor de relatório (conectar usando)**  
 Armazene um nome de usuário criptografado e a senha no banco de dados do servidor de relatórios. Escolha esta opção para executar um relatório autônomo (por exemplo, relatórios iniciados por agendas ou eventos em vez de ação do usuário). Se você estiver usando segurança padrão, o nome de usuário deve ser uma conta de domínio do Windows. Especifique a conta neste formato: \<domínio >\\< nome de usuário\>. A conta especificada deve ter permissões locais de logon no computador que hospeda a fonte de dados usada pelo relatório.  
  
 Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados** se as credenciais forem credenciais de Autenticação do Windows. Não selecione essa caixa de seleção se você estiver usando a autenticação de banco de dados (por exemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação).  
  
 Se você estiver usando a autenticação de banco de dados, selecione **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados** para permitir a delegação de credenciais de banco de dados, mas somente se um servidor de banco de dados der suporte à representação. Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bancos de dados, essa opção define a função SETUSER.  
  
 **Segurança integrada do Windows (conectar usando)**  
 Use as credenciais do Windows do usuário atual para acessar a fonte de dados. Selecione essa opção quando as credenciais usadas para acessar a fonte de dados forem as mesmas que as usadas para fazer logon no domínio de rede. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se a autenticação Kerberos não estiver habilitada, as credenciais do Windows poderão ser transmitidas para outro computador. Se forem necessárias conexões de computador adicionais, ocorrerá um erro em vez da exibição dos dados esperados.  
  
 Um administrador de servidor de relatórios pode desabilitar o uso da segurança integrada do Windows para acessar fontes de dados de relatório. Se esse valor estiver esmaecido, o recurso não estará disponível.  
  
 Não use essa opção se você planeja programar ou assinar a esse relatório. Processamento de relatório programado ou autônomo requer credenciais que podem ser obtidas sem entrada de usuário ou contexto de segurança de um usuário atual. Somente credenciais armazenadas fornecem esse recurso. Por esse motivo, o servidor de relatórios evita que você agende relatório ou processe assinatura, se o relatório estiver configurado para tipo de credencial de segurança integrada do Windows. Se você escolher essa opção para um relatório já assinado ou com operações agendadas, as operações de assinatura e agendamento serão interrompidas.  
  
 **Não são necessárias credenciais (conectar usando)**  
 Especifique que não são necessárias credenciais para acessar a fonte de dados. Observe que se uma fonte de dados necessitar de um logon de usuário, a escolha dessa opção não terá nenhum efeito. Você só deve escolher esta opção se a conexão de fonte de dados não requerer credenciais de usuário.  
  
 Para usar essa opção, a conta de execução autônoma deve estar previamente configurada para sua implantação de servidor de relatórios. A conta de execução autônoma é usada para conectar a fontes externas, quando outras fontes de credenciais não estiverem disponíveis. Se você especificar essa opção e a conta não estiver configurada, a conexão com a fonte de dados do relatório falhará e o processamento do relatório não ocorrerá. Para obter mais informações sobre essa conta, consulte [configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **OK**  
 Clique para salvar as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página de conteúdo &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
