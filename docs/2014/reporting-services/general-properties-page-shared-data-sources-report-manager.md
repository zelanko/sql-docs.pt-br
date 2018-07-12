---
title: Página Propriedades gerais, fontes de dados (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1b344449-6f7c-47d2-a737-972d88c0faf8
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2b729c41bf0ed0950c20b465bd1f0c70ebbee4a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162277"
---
# <a name="general-properties-page-shared-data-sources-report-manager"></a>Página Propriedades Gerais, fontes de dados compartilhadas (Gerenciador de Relatórios)
  Use a página Propriedades Gerais para exibir ou modificar propriedades de um item de fonte de dados compartilhada. Quaisquer alterações feitas nas propriedades serão efetivadas em todos os relatórios que referenciarem o item quando você clicar em **Aplicar**.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-general-properties-page-for-a-shared-data-source"></a>Para abrir a página Propriedades gerais de uma fonte de dados compartilhada  
  
1.  Abra o Gerenciador de Relatórios e localize a fonte de dados compartilhada cujas propriedades você deseja exibir.  
  
2.  Focalize a fonte de dados e clique na seta para baixo.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página Propriedades gerais da fonte de dados compartilhada.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica um nome para a fonte de dados compartilhada, que é usado para identificar o item no namespace do servidor de relatório.  
  
 **Descrição**  
 Fornece informações sobre a fonte de dados compartilhada. Essa descrição é exibida na página Conteúdo.  
  
 **Ocultar na exibição de lista**  
 Selecione essa opção para ocultar a fonte de dados compartilhada de usuários que estão usando o modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando se navega na hierarquia de pastas do servidor de relatórios. Na exibição de lista, os nomes de itens e as descrições fluem pela página. O formato alternativo é o modo de exibição de detalhes. A exibição de detalhes omite descrições, mas contém outras informações sobre o item. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Se quiser restringir o acesso a um item, você precisará criar uma atribuição de função.  
  
 **Habilitar esta fonte de dados**  
 Selecione para habilitar ou desabilitar a fonte de dados compartilhada. Você pode desabilitar a fonte de dados compartilhada para evitar o processamento de todos os relatórios, modelos de relatório e assinaturas controladas por dados que referenciam o item.  
  
 **Tipo de fonte de dados**  
 Especifica a extensão do processamento de dados usada para processar dados da fonte de dados. O servidor de relatório inclui extensões de processamento de dados para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, XML, SAP, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], ODBC e OLE DB. Extensões de processamento de dados adicionais podem estar disponíveis em fornecedores de terceiros.  
  
 Observe que, se estiver usando o [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] Edition com Advanced Services, você só poderá escolher fontes de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Cadeia de conexão**  
 Especifique a cadeia de conexão que o servidor de relatório utiliza para conectar-se à fonte de dados. O tipo de conexão determina a sintaxe que você deve usar. Por exemplo, uma cadeia de caracteres de conexão da extensão do processamento de dados XML é uma URL para um documento XML. Na maioria dos casos, uma cadeia de caracteres de conexão típica especifica o servidor de banco de dados e um arquivo de dados. O exemplo a seguir ilustra uma cadeia de caracteres de conexão usada para conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] banco de dados:  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 **Conecte-se usando**  
 Especifica opções que determinam como as credenciais são obtidas.  
  
> [!IMPORTANT]  
>  Se forem fornecidas credenciais na cadeia de conexão, serão ignorados as opções e os valores fornecidos nesta seção. Observe que, se você especificar as credenciais na cadeia de conexão, os valores serão exibidos em texto não criptografado para todos os usuários que exibirem essa página.  
  
 **Credenciais fornecidas pelo usuário que executa o relatório**  
 Cada usuário deve digitar um nome de usuário e uma senha para acessar a fonte de dados. Você pode definir o texto do prompt que solicita as credenciais do usuário. A cadeia de caracteres de texto padrão é "Digite um nome de usuário e uma senha para acessar a fonte de dados".  
  
 Selecione **Usar como credenciais do Windows ao conectar à fonte de dados** se as credenciais que o usuário fornece forem credenciais de Autenticação do Windows. Não marque esta caixa de seleção se você estiver usando autenticação de banco de dados (por exemplo, Autenticação do SQL Server).  
  
 **Credenciais armazenadas com segurança no servidor de relatório**  
 Armazene um nome de usuário criptografado e a senha no banco de dados do servidor de relatórios. Selecione essa opção para executar um relatório autônomo (por exemplo, relatórios iniciados por agendas ou eventos em vez de pela ação do usuário). Se você estiver usando segurança padrão, o nome de usuário deve ser uma conta de domínio do Windows. Especifique a conta neste formato: \<domínio >\\< nome de usuário\>. A conta especificada deve ter permissões locais de logon no computador que hospeda a fonte de dados usada pelo relatório.  
  
 Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados** se as credenciais forem credenciais de Autenticação do Windows. Não selecione essa caixa de seleção se você estiver usando a autenticação de banco de dados (por exemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação).  
  
 Se você estiver usando autenticação de banco de dados, selecione **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados (Conectar usando)** para permitir delegação de credenciais de banco de dados, mas somente se um servidor de banco de dados oferecer suporte a representação. Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bancos de dados, essa opção define a função SETUSER.  
  
 **Segurança integrada do Windows**  
 Use as credenciais do Windows do usuário atual para acessar a fonte de dados. Selecione essa opção quando as credenciais usadas para acessar a fonte de dados forem as mesmas que as usadas para fazer logon no domínio de rede. Esta opção funciona melhor quando a autenticação Kerberos está habilitada para o seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se Kerberos não estiver habilitado, as credenciais do Windows poderão ser passadas para outro computador. Se forem necessárias conexões de computador adicionais, ocorrerá um erro em vez da exibição dos dados esperados.  
  
 Um administrador de servidor de relatórios pode desabilitar o uso da segurança integrada do Windows para acessar fontes de dados de relatório. Se esse valor estiver esmaecido, o recurso não estará disponível.  
  
 Não use essa opção se você planeja programar ou assinar a esse relatório. Processamento de relatório programado ou autônomo requer credenciais que podem ser obtidas sem entrada de usuário ou contexto de segurança de um usuário atual. Somente credenciais armazenadas fornecem esse recurso. Por esse motivo, o servidor de relatórios evita que você agende relatório ou processe assinatura, se o relatório estiver configurado para tipo de credencial de segurança integrada do Windows. Se você escolher essa opção para um relatório já assinado ou com operações agendadas, as operações de assinatura e agendamento serão interrompidas.  
  
 **Não são necessárias credenciais**  
 Especifique que não são necessárias credenciais para acessar a fonte de dados. Observe que se uma fonte de dados necessitar de um logon de usuário, a escolha dessa opção não terá nenhum efeito. Você só deve escolher esta opção se a conexão de fonte de dados não requerer credenciais de usuário.  
  
 Para usar essa opção, a conta de execução autônoma deve estar previamente configurada para sua implantação de servidor de relatórios. A conta de execução autônoma é usada para conectar a fontes externas, quando outras fontes de credenciais não estiverem disponíveis. Se você especificar essa opção e a conta não estiver configurada, a conexão com a fonte de dados do relatório falhará e o processamento do relatório não ocorrerá. Para obter mais informações sobre essa conta, consulte [configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
 **Delete (excluir)**  
 Clique para excluir a fonte de dados compartilhada. A exclusão de uma fonte de dados compartilhada desativa quaisquer relatórios, modelos e assinaturas controladas por dados que a utilizam. Para reativar relatórios, modelos e assinaturas, é necessário abrir cada um e suas propriedades de fontes de dados para usar uma fonte de dados compartilhada diferente. Para relatórios e assinaturas, você pode especificar informações de conexão de fonte de dados como valores de propriedade de Fonte de Dados.  
  
 **Migrar**  
 Clique para mover a fonte de dados compartilhada para outro local no namespace da pasta de servidor de relatório.  
  
 **Gerar modelo**  
 Clique para criar um modelo novo com base na fonte de dados compartilhada.  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página Nova Fonte de Dados &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
