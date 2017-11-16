---
title: "Definir opções de representação (SSAS - Multidimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords:
- Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9dfd1dbf5f4f514136695dc2bb0d776afda99562
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-impersonation-options-ssas---multidimensional"></a>Definir opções de representação (SSAS multidimensional)
  Ao criar um objeto **data source** em um modelo do Analysis Services, uma das configurações que você deve configurar é uma opção de representação. Esta opção determina se o Analysis Services assume a identidade de uma conta de usuário do Windows específica ao executar operações locais relacionadas à conexão, como carregar um provedor de dados OLE DB ou resolver informações de perfil de usuário em ambientes que dão suporte a perfis móveis.  
  
 Para conexões que usam a autenticação do Windows, a opção de representação também determina a identidade de usuário sob a qual as consultas são executadas na fonte de dados externa. Por exemplo, se você definir a opção de representação como **contoso\dbuser**, as consultas usadas para recuperar os dados durante o processamento serão executadas como **contoso\dbuser** no servidor de banco de dados.  
  
 Este tópico explica como definir as opções de representação na caixa de diálogo **Informações sobre Representação** ao configurar um objeto de fonte de dados.  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>Definir opções de representação nas Ferramentas de Dados do SQL Server  
  
1.  Clique duas vezes em uma fonte de dados no Gerenciador de Soluções para abrir o Designer da Fonte de Dados.  
  
2.  Clique na guia **Informações sobre Representação** no Designer da Fonte de Dados.  
  
3.  Escolha uma opção descrita em [Opções de representação](#bkmk_options) neste tópico.  
  
## <a name="set-impersonation-options-in-management-studio"></a>Definir opções de representação no Management Studio  
 No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra a caixa de diálogo **Informações sobre Representação** clicando no botão de reticências (**...**) das seguintes propriedades destas caixas de diálogo:  
  
-   Caixa de diálogo**Propriedades de Banco de Dados** , por meio da propriedade Informações sobre Representação de Fonte de Dados.  
  
-   Caixa de diálogo**Propriedades da Fonte de Dados** , por meio da propriedade Informações sobre Representação.  
  
-   Caixa de diálogo**Propriedades do Assembly** , por meio da propriedade Informações sobre Representação.  
  
##  <a name="bkmk_options"></a> Opções de representação  
 Todas as opções estão disponíveis na caixa de diálogo, mas nem todas as opções são apropriadas para todos os cenários. Use as informações a seguir para determinar a melhor opção para seu cenário.  
  
 **Usar nome de usuário e senha específicos**  
 Selecione esta opção para fazer o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto usar as credenciais de segurança de uma conta de usuário do Windows especificadas neste formato:  *\<nome de domínio >*  **\\**   *\<Nome de conta de usuário >*.  
  
 Escolha esta opção para usar uma identidade de usuário dedicada e com privilégios mínimos do Windows que você criou especificamente para finalidade de acesso a dados. Por exemplo, se você periodicamente criar uma conta de finalidade geral para recuperar dados usados em relatórios, poderá especificar essa conta aqui.  
  
 Para bancos de dados multidimensionais, as credenciais especificadas são usadas para processamento, consultas ROLAP, associações fora de linha, cubos locais, modelos de mineração, partições remotas, objetos vinculados e sincronização do destino para a origem.  
  
 Para instruções OPENQUERY DMX, essa opção é ignorada e as credenciais do usuário atual são usadas em vez da conta de usuário especificada.  
  
 **Usar a conta de serviço**  
 Selecione esta opção para fazer o objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usar as credenciais de segurança associadas ao serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que gerencia o objeto. Essa é a opção padrão. Em versões anteriores, esta era a única opção que você poderia usar. Você pode preferir esta opção para monitorar o acesso a dados no nível de serviço em vez de contas de usuário individuais.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], dependendo do sistema operacional que você estiver usando, a conta de serviço poderá ser NetworkService ou uma conta virtual interna criada para uma instância específica do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se você escolher a conta de serviço para uma conexão que usa a autenticação do Windows, lembre-se de criar um logon de banco de dados para essa conta e conceder permissões de leitura, pois ela será usada para recuperar dados durante o processamento. Para obter mais informações sobre a conta de serviço, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!NOTE]  
>  Ao usar a autenticação de banco de dados, você deverá escolher a opção de representação **Usar a conta de serviço** se o serviço estiver sendo executado sob a conta virtual dedicada para o Analysis Services. Esta conta terá permissões para acessar arquivos locais. Se o serviço for executado como NetworkService, uma alternativa melhor será usar uma conta de usuário do Windows com privilégios mínimos que tenha permissões **Permitir logon localmente** . Dependendo da conta que você fornecer, também poderá ser necessário conceder permissões de acesso ao arquivo na pasta do programa do Analysis Services.  
  
 Para bancos de dados multidimensionais, as credenciais da conta de serviço serão usadas para processamento, consultas ROLAP, partições remotas, objetos vinculados e sincronização do destino para a origem.  
  
 Para instruções OPENQUERY do DMX, cubos locais e modelos de mineração, as credenciais do usuário atual são usadas mesmo se você escolher uma opção da conta de serviço. A opção da conta de serviço não tem suporte para associações fora de linha.  
  
> [!NOTE]  
>  Poderão ocorrer erros durante o processamento de um modelo de mineração de dados em um cubo se a conta de serviço não tiver permissões de administrador na instância do Analysis Services. Para obter mais informações, consulte [Mining Structure: Issue while Processing when DataSource is OLAP Cube](http://go.microsoft.com/fwlink/?LinkId=251610)(Estrutura de mineração: problema durante o processamento quando DataSource é um cubo OLAP).  
  
 **Usar as credenciais do usuário atual**  
 Selecione esta opção para fazer com que o objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] use as credenciais de segurança do usuário atual para associações fora de linha, OPENQUERY DMX, cubos locais e modelos de mineração.  
  
 Com a exceção de cubos locais e processamento usando associações fora de linha, esta opção não tem suporte para bancos de dados multidimensionais.  
  
 **Padrão** ou **Herdar**  
 A caixa de diálogo usa **Padrão** para as opções de representação definidas no nível de banco de dados e **Herdar** para as opções de representação definidas no nível de fonte de dados.  
  
 **Fontes de dados – opção Herdar**  
  
 No nível da fonte de dados, **Herdar** especifica que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve usar a opção de representação do objeto pai. Em um modelo multidimensional, o objeto pai é o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Escolher a opção **Herdar** permite gerenciar centralmente as configurações de representação para essa e outras fontes de dados que fazem parte do mesmo banco de dados. Para que esta opção seja significativa, escolha um nome de usuário e senha específicos do Windows no nível do banco de dados. Caso contrário, a combinação de **Herdar** na fonte de dados e **Padrão** no banco de dados é equivalente a usar a opção da conta de serviço.  
  
 Para especificar um nome de usuário e senha do Windows no nível do banco de dados, faça o seguinte:  
  
1.  Clique com o botão direito do mouse no banco de dados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e selecione **Propriedades**.  
  
2.  Em **Informações sobre Representação da Fonte de Dados**, especifique um nome de usuário e senha do Windows.  
  
3.  Clique com o botão direito do mouse em cada fonte de dados e exiba suas propriedades para garantir que cada uma esteja usando a opção **Herdar**.  
  
 Para obter mais informações sobre as configurações padrão no nível do banco de dados, consulte [Definir propriedades do Banco de Dados Multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md).  
  
 **Bancos de dados – opção Padrão**  

 Para bancos de dados multidimensionais, **Padrão** significa o uso da conta de serviço e do usuário atual para operações de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Definir propriedades da fonte de dados &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)   

  
  

