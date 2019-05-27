---
title: Excluir e recriar chaves de criptografia (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c293b7007ccb8a42928c02ed37bcaacb898504f9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108695"
---
# <a name="delete-and-re-create-encryption-keys--ssrs-configuration-manager"></a>Excluir e recriar chaves de criptografia (Gerenciador de configurações do SSRS)
  A exclusão e a recriação de chaves de criptografia são atividades que estão fora da manutenção rotineira da chave de criptografia. Você executa essas tarefas em resposta a uma ameaça específica ao seu servidor de relatórios ou como um último recurso quando não mais puder acessar um banco de dados de servidor de relatórios.  
  
-   Recrie a chave simétrica quando você acreditar que a chave simétrica existente está comprometida. Você também pode recriar a chave regularmente como uma prática recomendada de segurança.  
  
-   Exclua as chaves de criptografia existentes e conteúdo criptografado inutilizável quando você não puder restaurar a chave simétrica.  
  
## <a name="re-creating-encryption-keys"></a>recriando chaves de criptografia  
 Se você tiver evidências de que a chave simétrica é conhecida por usuários não autorizados ou se o servidor de relatórios esteve sob ataque e você deseja redefinir a chave simétrica como uma precaução, poderá recriar a chave simétrica. Quando você recria a chave simétrica, todos os valores criptografados serão criptografados novamente usando o novo valor. Se estiver executando vários servidores de relatório em uma implantação de expansão, todas as cópias da chave simétrica serão atualizadas para o novo valor. O servidor de relatórios usa as chaves públicas disponíveis para ele a fim de atualizar a chave simétrica para cada servidor na implantação.  
  
 Você poderá recriar a chave simétrica somente quando o servidor de relatórios se encontrar em um estado de funcionamento. Recriar as chaves de criptografia e criptografar novamente o conteúdo interrompe as operações do servidor. Você deve colocar o servidor offline enquanto a nova criptografia estiver em andamento. Não deve haver nenhuma solicitação feita ao servidor de relatórios durante a nova criptografia.  
  
 Você pode usar a ferramenta Configuração do Reporting Services ou o utilitário **rskeymgmt** para redefinir a chave simétrica e os dados criptografados. Para obter mais informações sobre como a chave simétrica é criada, consulte [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-initialize-a-report-server.md).  
  
#### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>Como recriar chaves de criptografia (ferramenta Configuração do Reporting Services)  
  
1.  Desabilite o serviço Web Servidor de Relatórios e o acesso ao HTTP modificando a propriedade `IsWebServiceEnabled` no arquivo rsreportserver.config. Esta etapa interrompe temporariamente o envio das solicitações de autenticação ao servidor de relatórios sem desligar o servidor completamente. Você deve ter o mínimo de serviço de forma que possa recriar as chaves.  
  
     Se você estiver recriando chaves de criptografia para uma implantação de expansão do servidor de relatórios, desabilite essa propriedade em todas as instâncias na implantação.  
  
    1.  Abra o Windows Explorer e navegue até *unidade*:\Arquivos de Programas\Microsoft SQL Server\\*report_server_instance*\Reporting Services. Substitua *unidade* pela letra de sua unidade e *report_server_instance* pelo nome da pasta que corresponde à instância do servidor de relatórios para a qual deseja desabilitar o serviço Web e o acesso HTTP. Por exemplo, C:\Arquivos de Programas\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services.  
  
    2.  Abra o arquivo rsreportserver.config.  
  
    3.  Na propriedade `IsWebServiceEnabled`, especifique `False` e salve suas alterações.  
  
2.  Inicie a ferramenta Configuração do Reporting Services e conecte-se à instância do servidor de relatório que deseja configurar.  
  
3.  Na página Chaves de Criptografia, clique em **Alterar**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Reinicie o serviço do Windows Servidor de Relatórios. Se estiver recriando chaves de criptografia para uma implantação de expansão, reinicie o serviço em todas as instâncias.  
  
5.  Habilite novamente o serviço Web e o acesso HTTP modificando a propriedade `IsWebServiceEnabled` no arquivo rsreportserver.config. Faça isso para todas as instâncias se você estiver trabalhando com uma implantação de expansão.  
  
#### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>Como recriar chaves de criptografia (rskeymgmt)  
  
1.  Desabilite o serviço Web Servidor de Relatórios e o acesso HTTP. Use as instruções do procedimento anterior para interromper as operações do serviço Web.  
  
2.  Execute **rskeymgmt.exe** localmente no computador que hospeda o servidor de relatório. Use o argumento `-s` para redefinir a chave simétrica. Nenhum outro argumento é necessário:  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Reinicie o serviço do Windows e habilite as operações do serviço Web.  
  
## <a name="deleting-unusable-encrypted-content"></a>Excluindo conteúdo criptografado inutilizável  
 Se por alguma razão não for possível restaurar a chave de criptografia, o servidor de relatórios nunca poderá descriptografar e usar nenhum dado criptografado com essa chave. Para retornar o servidor de relatórios a um estado de funcionamento, você deve excluir os valores criptografados que atualmente estão armazenados no banco de dados do servidor de relatórios e depois especificar novamente manualmente os valores necessários.  
  
 A exclusão das chaves de criptografia remove todas as informações de chave simétrica do banco de dados do servidor de relatórios e exclui qualquer conteúdo criptografado. Todos os dados não criptografados são deixados intactos; somente o conteúdo criptografado é removido. Quando você exclui as chaves de criptografia, o servidor de relatórios é reinicializado automaticamente adicionando uma nova chave simétrica. Ocorrerá o seguinte quando você excluir conteúdo criptografado:  
  
-   As cadeias de caracteres de conexão em fontes de dados compartilhadas serão excluídas. Os usuários que executam relatórios obtêm o erro "A propriedade ConnectionString não foi inicializada".  
  
-   As credenciais armazenadas serão excluídas. Os relatórios e as fontes de dados compartilhadas serão reconfiguradas para usar credenciais solicitadas.  
  
-   Os relatórios com base em modelos (e que precisam de fontes de dados compartilhadas configuradas com credenciais armazenadas ou sem nenhuma) não serão executados.  
  
-   As assinaturas serão desativadas.  
  
 Depois de excluir conteúdo criptografado, você não poderá recuperá-lo. Você deve especificar novamente as cadeias de caracteres de conexão e credenciais armazenadas, e deve ativar assinaturas.  
  
 Você pode usar a ferramenta Configuração do Reporting Services ou o utilitário **rskeymgmt** para remover os valores.  
  
#### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>Como excluir chaves de criptografia (ferramenta Configuração do Reporting Services)  
  
1.  Inicie a ferramenta Configuração do Reporting Services e conecte-se à instância do servidor de relatório que deseja configurar.  
  
2.  Clique em **Chaves de Criptografia**e clique em **Excluir**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Reinicie o serviço do Windows Servidor de Relatórios. Para uma implantação de expansão, faça isso em todas as instâncias do servidor de relatórios.  
  
#### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>Como excluir chaves de criptografia (rskeymmgt)  
  
1.  Execute **rskeymgmt.exe** localmente no computador que hospeda o servidor de relatório. Você deve usar o argumento de aplicação **-d** . O exemplo a seguir ilustra o argumento que você deve especificar:  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  Reinicie o serviço do Windows Servidor de Relatórios. Para uma implantação de expansão, faça isso em todas as instâncias do servidor de relatórios.  
  
#### <a name="how-to-re-specify-encrypted-values"></a>Como especificar novamente valores criptografados  
  
1.  Para cada fonte de dados compartilhada, você deve digitar novamente a cadeia de caracteres de conexão.  
  
2.  Para cada relatório e fonte de dados compartilhada que use credenciais armazenadas, você deve digitar novamente o nome do usuário e a senha e depois salvar. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../integration-services/connection-manager/data-sources.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Para cada assinatura controlada por dados, abra cada assinatura e digite novamente as credenciais do banco de dados de assinatura.  
  
4.  Para assinaturas que usam dados criptografados (isso inclui a extensão de entrega Compartilhamento de Arquivos e qualquer extensão de entrega de terceiros que use criptografia), abra cada assinatura e digite novamente as credenciais. As assinaturas que usam a entrega de email do Servidor de Relatórios não usam dados criptografados e não são afetadas pela alteração da chave.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de configurações do SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
