---
title: Conta de execução (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9ba41b602ec91516e87b7fe5ec0276c586b17613
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989030"
---
# <a name="execution-account-ssrs-native-mode"></a>Conta de execução (modo nativo do SSRS)
  Use esta página para configurar uma conta a ser usada para processamento autônomo. Essa conta é usada em circunstâncias especiais, quando outras fontes de credenciais não estiverem disponíveis:  
  
-   Quando o servidor de relatório se conecta a uma fonte de dados que não requer credenciais. Exemplos de fontes de dados que podem não requerer credenciais incluem documentos XML e alguns aplicativos de banco de dados do lado do cliente.  
  
-   Quando o servidor de relatório se conecta a outro servidor para recuperar arquivos de imagem externos ou outros recursos que são referenciados em um relatório.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A configuração dessa conta é opcional, mas não configurá-la limita seu uso de imagens externas e conexões com algumas fontes de dados. Ao recuperar arquivos de imagem externos, o servidor de relatório verifica se uma conexão anônima pode ser feita. Se a conexão for protegida por senha, o servidor de relatório usa a conta de processamento autônomo de relatórios para conectar-se ao servidor remoto. Ao recuperar dados de um relatório, o servidor de relatório representa o usuário atual, solicita ao usuário que forneça credenciais, usa credenciais armazenadas ou usa a conta de processamento autônomo se a conexão da fonte de dados especificar **Nenhum** como o tipo de credencial. O servidor de relatório não permite que as credenciais de sua conta de serviço sejam delegadas ou representadas ao conectar-se a outros computadores, portanto ele deverá usar a conta de processamento autônomo se nenhuma outra credencial estiver disponível.  
  
 A conta que você especifica deve ser diferente da usada para executar a conta de serviço. Se você configurar essa conta, ela será armazenada no arquivo RSReportServer.config como um valor criptografado. Se você estiver executando o servidor de relatório em uma implantação de expansão, deverá configurar essa conta da mesma maneira em cada servidor de relatório.  
  
 Você pode usar qualquer conta de usuário do Windows. Para obter melhores resultados, escolha uma conta que tenha permissões de leitura e permissões de logon na rede a fim de dar suporte a conexões com outros computadores. Ela deve ter a permissão de leitura em qualquer imagem externa ou arquivo de dados que você deseja usar em um relatório. Não especifique uma conta local, a menos que todas as fontes de dados do relatório e imagens externas estejam armazenadas no computador do servidor de relatório. Use a conta somente para o processamento autônomo de relatórios.  
  
> [!NOTE]  
>  Se você estiver utilizando o [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] com Advanced Services, deverá configurar esta conta somente se estiver referenciando imagens externas em um relatório e for exigida permissão para acessar o arquivo de imagem. O SQL Server Express não dá suporte a uma conexão de fonte de dados a um servidor remoto. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 Para abrir esta página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selecione **Conta de Execução** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Especificar uma conta de execução**  
 Selecione para especificar uma conta.  
  
 **Conta**  
 Insira uma conta de usuário de domínio do Windows. Use este formato: *\<domain>\\<user account\>*.  
  
 **Senha**  
 Digite a senha.  
  
 **Confirmar senha**  
 Redigite a senha.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Configurar a conta de execução autônoma &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
