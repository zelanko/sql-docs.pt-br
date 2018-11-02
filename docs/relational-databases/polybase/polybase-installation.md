---
title: Instalar o PolyBase no Windows | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, installation
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e30cded830401c589c62d1e6301d5be78720c07f
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806746"
---
# <a name="install-polybase-on-windows"></a>Instalar o PolyBase no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para instalar uma versão de avaliação do SQL Server, vá para [avaliações do SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016). 
   
## <a name="prerequisites"></a>Prerequisites  
   
- Edição de avaliação do SQL Server de 64 bits  
   
- Microsoft .NET Framework 4.5.  

- Oracle JRE (Java SE Runtime Environment). Há suporte para as versões 7 (a partir de 7.51) e 8 (o [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) ou o [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funcionará). Vá para [Downloads de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html). O instalador falhará se o JRE não estiver presente. Não há suporte para o JRE9 e o JRE10.

- Memória mínima: 4 GB  
   
- Espaço mínimo no disco rígido: 2 GB  
- **Recomendado:** mínimo de 16 GB de RAM
   
- O TCP/IP deve estar habilitada para o Polybase para funcionar corretamente. O TCP/IP está habilitado por padrão em todas as edições do SQL Server, exceto nas edições Developer e Express do SQL Server. Para que o Polybase funcione corretamente nas edições Developer e Express, é necessário habilitar a conectividade TCP/IP (consulte [Habilitar ou Desabilitar um Protocolo de Rede do Servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)).

- MSVC++ 2012 

**Observação**  

O PolyBase pode ser instalado apenas em uma instância SQL Server por computador.

> **Importante**
>
> Se você pretende usar a funcionalidade de aplicação de computação no Hadoop, garanta que o cluster do Hadoop de destino tenha os componentes principais do HDFS, YARN/MapReduce com o servidor Jobhistory habilitado. O PolyBase envia a consulta de aplicação via MapReduce e recebe o status do servidor JobHistory. A consulta falhará se não tiver um desses componentes.
  
## <a name="single-node-or-polybase-scaleout-group"></a>Nó único ou grupo ScaleOut do PolyBase

Antes de iniciar a instalação do PolyBase em suas Instâncias do SQL Server, planeje se você desejará uma instalação de nó único ou um [grupo de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).

Para um grupo de expansão do PolyBase, você precisará garantir que:

- Todos os computadores estão no mesmo domínio.
- Use a mesma conta de serviço e senha durante a instalação do PolyBase.
- As Instâncias do SQL Server podem se comunicar entre si pela rede.
- As instâncias do SQL Server são todas da mesma versão do SQL Server.

Depois de instalar o PolyBase como um grupo autônomo ou de expansão, não é possível fazer alterações. Você precisará desinstalar e reinstalar o recurso para alterar essa configuração.

## <a name="install-using-the-installation-wizard"></a>Instalar usando o assistente de instalação  
   
1. Execute o setup.exe do SQL Server.   
   
2. Clique em **Instalação**, em **Nova instalação autônoma do SQL Server ou adicionar recursos**.  
   
3. Na página de seleção de recursos, escolha **Serviço de Consulta do PolyBase para Dados Externos**.  

 ![Serviços do PolyBase](../../relational-databases/polybase/media/install-wizard.png "Serviços do PolyBase")  
   
4. Na página Configuração do Servidor, defina o **Serviço Mecanismo PolyBase do SQL Server** e o Serviço Movimentação de Dados PolyBase do SQL Server para serem executados na mesma conta de domínio.  
   
 > **IMPORTANTE:** 
>
>Em um grupo de escala horizontal do PolyBase, o serviço de movimentação de dados e de mecanismo de PolyBase em todos os nós devem ser executados na mesma conta de domínio. Confira [Grupos de escala horizontal do PolyBase](#Enable)
   
5. Na página **Configuração do PolyBase**, escolha uma das duas opções. Consulte [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md) para obter mais informações.  
   
   - Use a instância do SQL Server como uma instância habilitada para PolyBase autônoma.  
   
     Escolha essa opção para usar a instância do SQL Server como um nó de cabeçalho autônomo.  
   
   - Use a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase.  A seleção dessa opção abre o firewall para permitir conexões de entrada com o Mecanismo de Banco de Dados do SQL Server, o Mecanismo PolyBase do SQL Server, o serviço Movimentação de Dados PolyBase do SQL Server e o SQL Browser. O firewall é aberto para permitir conexões de entrada de outros nós em um grupo de escala horizontal de PolyBase.  
   
     Esta opção também habilita conexões de firewall do MSDTC (Coordenador de Transações Distribuídas da Microsoft) e modifica as configurações de registro do MSDTC.  
   
6. Na **página Configuração do PolyBase**, especifique um intervalo de portas com pelo menos seis portas. A instalação do SQL Server alocará as primeiras seis portas disponíveis do intervalo.  

  > **IMPORTANTE:**
  >
  > Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).


##  <a name="installing"></a> Instalar usando um prompt de comando  

Use os valores nesta tabela para criar scripts de instalação. Os dois serviços, **Mecanismo de PolyBase do SQL Server** e **Serviço de Movimentação de Dados de PolyBase do SQL Server** devem ser executados na mesma conta. Em um grupo de escala horizontal do PolyBase, os serviços do PolyBase em todos os nós devem ser executados na mesma conta de domínio.  
   
<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017"

|Componente do SQL Server|Parâmetro e valores|Descrição|  
|--------------------------|--------------------------|-----------------|  
|Controle de instalação do SQL Server|**Required**<br /><br /> /FEATURES=PolyBase|Seleciona o recurso PolyBase.|  
|Mecanismo de PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCACCOUNT|Especifica a conta do serviço de mecanismo. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCPASSWORD|Especifica a senha da conta de serviço de mecanismo.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCSTARTUPTYPE|Especifica o modo de inicialização do serviço de mecanismo PolyBase: Automático (padrão), Desabilitado e Manual|  
|Serviço de Movimentação de Dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCACCOUNT|Especifica a conta do serviço de movimentação de dados. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Serviço de movimentação de dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCPASSWORD|Especifica a senha para a conta de movimentação de dados.|  
|Serviço de movimentação de dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Especifica o modo de inicialização para o serviço de movimentação de dados: Automático (padrão), Desabilitado e Manual|  
|PolyBase|**Opcional**<br /><br /> /PBSCALEOUT|Especifica se a instância do SQL Server será usada como parte do grupo computacional de escala horizontal do PolyBase. <br />Valores com suporte: **True**, **False**|  
|PolyBase|**Opcional**<br /><br /> /PBPORTRANGE|Especifica um intervalo de portas com pelo menos 6 portas para serviços do PolyBase. Exemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

|Componente do SQL Server|Parâmetro e valores|Descrição|  
|--------------------------|--------------------------|-----------------|  
|Controle de instalação do SQL Server|**Necessário**<br /><br /> /FEATURES=PolyBaseCore, PolyBaseJava, PolyBase | **PolyBaseCore** instala o suporte para todos os recursos do PolyBase, exceto pela conectividade do Hadoop. **PolyBaseJava** habilita a conectividade do Hadoop. **PolyBase** instala ambos. |  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCACCOUNT|Especifica a conta do serviço de mecanismo. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCPASSWORD|Especifica a senha da conta de serviço de mecanismo.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCSTARTUPTYPE|Especifica o modo de inicialização do serviço de mecanismo PolyBase: Automático (padrão), Desabilitado e Manual|  
|Serviço de Movimentação de Dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCACCOUNT|Especifica a conta do serviço de movimentação de dados. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Serviço de movimentação de dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCPASSWORD|Especifica a senha para a conta de movimentação de dados.|  
|Serviço de movimentação de dados de PolyBase do SQL Server|**Opcional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Especifica o modo de inicialização para o serviço de movimentação de dados: Automático (padrão), Desabilitado e Manual|  
|PolyBase|**Opcional**<br /><br /> /PBSCALEOUT|Especifica se a instância do SQL Server será usada como parte do grupo computacional de escala horizontal do PolyBase. <br />Valores com suporte: **True**, **False**|  
|PolyBase|**Opcional**<br /><br /> /PBPORTRANGE|Especifica um intervalo de portas com pelo menos 6 portas para serviços do PolyBase. Exemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end

Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).



**Exemplo**

Mostra um exemplo de script de instalação.  

```cmd
   
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
   
```  

## <a id="enable"></a> Habilitar o PolyBase

Depois que você concluir a instalação, o Polybase deverá ser habilitado para acessar suas funcionalidades. conectar-se ao SQL Server 2019 CTP 2.0, você precisa habilitar o PolyBase após a instalação usando o seguinte comando Transact-SQL:


```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [ WITH OVERRIDE ]  ;
```
A instância, em seguida, precisa ser **reiniciada** 


## <a name="post-installation-notes"></a>Notas de pós-instalação  

O PolyBase instala três bancos de dados de usuário: DWConfiguration, DWDiagnostics e DWQueue.   Eles são para uso do PolyBase e devem não ser alterados ou excluídos.  
   
### <a id="confirminstall"></a> Como confirmar a instalação  

Execute o comando a seguir. Se o PolyBase estiver instalado, retornará 1; caso contrário, 0.  

```sql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  

### <a name="firewall-rules"></a>Regras de firewall  

A instalação do PolyBase do SQL Server cria as seguintes regras de firewall no computador.  
   
- PolyBase do SQL Server – Mecanismo de Banco de Dados – \<SQLServerInstanceName> (TCP-In)  
   
- PolyBase do SQL Server – Serviços do PolyBase – \<SQLServerInstanceName> (TCP-In)  

- PolyBase do SQL Server – Navegador do SQL – (UDP-In)  
   
Durante a instalação, se você escolher usar a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase, essas regras serão habilitadas e o firewall será aberto para permitir conexões de entrada com o Mecanismo de Banco de Dados do SQL Server, o Mecanismo PolyBase do SQL Server o serviço Movimentação de Dados PolyBase do SQL Server e o SQL Browser. No entanto, se o serviço de firewall no computador não estiver em execução durante a instalação, a instalação do SQL Server falhará ao habilitar essas regras. Nesse caso, você deve iniciar o serviço de Firewall no computador e habilitar pós-instalação essas regras.  
   
#### <a name="to-enable-the-firewall-rules"></a>Para habilitar as regras de firewall  

- Abra o **Painel de Controle**.  

- Clique em **Sistema e Segurança**e depois em **Firewall do Windows**.  
   
- Clique em **Configurações Avançadas**e em **Regras de entrada**.  
   
- Clique com o botão direito do mouse na regra desabilitada e depois clique em **Habilitar regra**.  
   
### <a name="polybase-service-accounts"></a>Contas de serviço do PolyBase

Para alterar as contas de serviço para o Mecanismo de PolyBase e os Serviços de Movimentação de Dados do PolyBase, desinstale e reinstale o recurso PolyBase.

## <a name="next-steps"></a>Próximas etapas  

Veja [Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md).
