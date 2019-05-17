---
title: Definir limites de aviso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbmmonitor.setwarningthreshold.f1
ms.assetid: 17f93147-e7d9-4092-b4c2-c11b38051171
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f1c7c05a02c67fda968ea26bd114d16b0b73925
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805159"
---
# <a name="set-warning-thresholds"></a>Configurar limites de aviso
  Use essa caixa de diálogo para habilitar e configurar um ou mais limites de aviso para o banco de dados selecionado na árvore de navegação da caixa de diálogo **Monitor de Espelhamento de Banco de Dados** .  
  
 A caixa de diálogo tenta se conectar a ambas as instâncias do servidor. Essas conexões são assincronamente estabelecidas. A caixa de diálogo mostra o status da conexão de cada parceiro. Se o parceiro não estiver conectado, você poderá clicar em **Conectar**.  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 *A instância de servidor e seu status de conexão*  
 Nome de uma instância de servidor de parceiro no formato _SYSTEM_**\\**_INSTANCE_NAME_. Com relação a uma instância de servidor padrão, o nome do sistema é exibido.  
  
 Esse campo indica também se o monitor está conectado atualmente à instância de servidor. Os status de conexão possíveis são:  
  
-   **Não conectado a**  *server_instance_name*  
  
-   **Tentando se conectar a**  *server_instance_name*  
  
-   **Conectado a**  *server_instance_name*  
  
    > [!NOTE]  
    >  Se você não for um membro da função de servidor fixa **sysadmin** , esse status será **Conectado a** *server_instance_name* **(Permissões limitadas)**.  
  
 O nome de cada uma das instâncias de servidor de parceiro é exibido em um campo separado de *Instância de servidor e status de conexão* . O campo superior relacionará o servidor principal quando o monitor começar a ser executado.  
  
 **Conectar**/**Cancelar**  
 O botão **Conectar**/**Cancelar** é associado a cada um dos campos *Instância de servidor e seu status de conexão* . O status do botão depende do status da conexão:  
  
-   Se não houver nenhuma conexão com a instância de servidor, o texto do botão será **Conectar**. Clique para estabelecer conexão com a instância de servidor.  
  
-   Quando uma tentativa de conexão estiver em andamento, o texto do botão será **Cancelar**. Clique para cancelar a tentativa de conexão.  
  
-   Se o servidor estiver conectado, o texto do botão será **Conectado**, e o botão ficará esmaecido.  
  
 **Limites**  
 A grade **Limites** exibe as configurações de avisos de duas instâncias de servidor.  
  
> [!NOTE]  
>  Se uma instância de servidor não estiver conectada, suas colunas serão exibidas com células vazias e um plano de fundo cinza. Quando a conexão for aberta, a grade exibirá automaticamente o conteúdo da instância.  
  
 A grade contém as seguintes colunas:  
  
 **Warnings**  
 Relaciona os avisos que têm suporte:  
  
|Aviso|Descrição|  
|-------------|-----------------|  
|**Avisar se o log não enviado exceder o limite**|O limite indica o número de quilobytes (KB) do log não enviado na fila principal de envios de log.|  
|**Avisar se o log não restaurado exceder o limite**|O limite indica o número de KBs da fila de restauração na instância de servidor espelho.|  
|**Avisar se a idade da transação não enviada mais antiga exceder o limite**|O limite indica o número de minutos de transações que ainda não foram enviadas da fila de envio para a instância de servidor de espelho. Esse valor ajuda a medir o potencial de perda de dados em termos de tempo.|  
|**Avisar se a sobrecarga espelhada confirmada exceder o limite**|O limite indica o número de milissegundos de retardo por transação (pertinente só em modo de alta segurança). Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração.|  
  
 **Habilitado em “** *\<server instance>* **”**  
 Uma caixa de seleção em branco indica que o aviso está desabilitado presentemente na instância de servidor. Para habilitar um aviso, clique em sua caixa de seleção.  
  
 **Limite em “** *\<server instance>* **”**  
 Quando um aviso for habilitado, defina o limite no lado esquerdo dessa coluna. Um evento ocorrerá se o limite especificado tiver sido atingido quando a tabela de status for atualizada. Se você desabilitar um limite depois de configurar um valor, o valor permanecerá no campo e será usado quando você reabilitar o aviso.  
  
 Quando um aviso não for habilitado, o campo permanecerá inativo.  
  
 **OK**  
 Clicar em **OK** fecha essa caixa de diálogo e exibe os valores dos limites de aviso especificados atualmente na grade **Limites** na página com guias **Avisos**.  
  
## <a name="remarks"></a>Comentários  
 Um limite só se aplica a um parceiro por vez, mas é recomendado definir um limite para um determinado evento em ambos os parceiros, para assegurar que o aviso persista caso o banco de dados apresente failover. O limite adequado para cada parceiro depende das capacidades de desempenho o sistema daquele parceiro.  
  
 Um evento de desempenho é gravado no log de eventos somente se o seu valor estiver no seu limite ou acima dele quando a tabela de status for atualizada. Se um valor máximo alcançar temporariamente o limite entre as atualizações de status, este valor máximo é ignorado  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
  
