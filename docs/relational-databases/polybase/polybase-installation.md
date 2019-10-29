---
title: Instalar o PolyBase no Windows | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, installation
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 007719c2407f6e193b8612ef51944ccbfd3238d3
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908666"
---
# <a name="install-polybase-on-windows"></a>Instalar o PolyBase no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para instalar uma versão de avaliação do SQL Server, vá para [avaliações do SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016). 
   
## <a name="prerequisites"></a>Prerequisites  
   
- Edição de Avaliação do SQL Server de 64 bits.  
   
- Microsoft .NET Framework 4.5.  

- Memória mínima: 4 GB. 
   
- Espaço mínimo no disco rígido: 2 GB.
  
- Recomendado: Mínimo de 16 GB de RAM.
   
- O TCP/IP deve estar habilitado para o PolyBase para funcionar corretamente. O TCP/IP está habilitado por padrão em todas as edições do SQL Server, exceto nas edições Developer e Express do SQL Server. Para que o PolyBase funcione corretamente nas edições Developer e Express, é necessário habilitar a conectividade TCP/IP. Veja [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


>[!NOTE] 
> O PolyBase pode ser instalado apenas em uma instância SQL Server por computador.


>[!NOTE]
>Para usar o PolyBase, você deve permissões no nível de sysadmin ou SERVER CONTROL no banco de dados.

>[!IMPORTANT]
>Para usar a funcionalidade de aplicação de computação no Hadoop, o cluster do Hadoop de destino deve ter os componentes principais do HDFS, YARN e MapReduce, com o servidor de histórico de trabalhos habilitado. O PolyBase envia a consulta de aplicação via MapReduce e recebe o status do servidor de histórico de trabalhos. A consulta falhará se não tiver um desses componentes.
  
## <a name="single-node-or-polybase-scale-out-group"></a>Nó único ou grupo de escala horizontal do PolyBase

Antes de instalar PolyBase em suas instâncias do SQL Server, decida por uma instalação de nó único ou um [grupo de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).

Em um grupo de escala horizontal do PolyBase, verifique se:

- Todos os computadores estão no mesmo domínio.
- Use a mesma conta de serviço e senha durante a instalação do PolyBase.
- As Instâncias do SQL Server podem se comunicar entre si pela rede.
- As instâncias do SQL Server são todas da mesma versão do SQL Server.

Depois de instalar o PolyBase autônomo ou em um grupo de escala horizontal, você não poderá alterar. Para alterar essa configuração, você terá que desinstalar e reinstalar o recurso.

## <a name="use-the-installation-wizard"></a>Use o assistente de instalação
   
1. Execute o setup.exe do SQL Server.   
   
2. Selecione **Instalação** e **Nova instalação autônoma do SQL Server ou adicionar recursos**.  
   
3. Na página Seleção de Recursos, escolha **Serviço de Consulta do PolyBase para Dados Externos**.  

   ![Serviços PolyBase](../../relational-databases/polybase/media/install-wizard.png "Serviços PolyBase")  
   
   >[!NOTE]
   >O PolyBase do SQL Server 2019 agora inclui uma opção adicional **Conector Java para fonte de dados HDFS**. Confira os [recursos da versão prévia do SQL Server](https://cloudblogs.microsoft.com/sqlserver/2019/04/24/sql-server-2019-community-technology-preview-2-5-is-now-available/) para obter mais informações sobre esse recurso.
   
4. Na página Configuração do Servidor, defina o **Serviço do Mecanismo PolyBase do SQL Server** e o **Serviço de Movimentação de Dados PolyBase do SQL Server** para serem executados na mesma conta de domínio.  

   >[!IMPORTANT]
   >Em um grupo de escala horizontal do PolyBase, o serviço de Movimentação de Dados e de Mecanismo de PolyBase em todos os nós devem ser executados na mesma conta de domínio. Confira [Grupos de escala horizontal do PolyBase](#enable).

5. Na página Configuração do PolyBase, escolha uma das duas opções. Para obter mais informações, confira [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  
   
   - Use a instância do SQL Server como uma instância habilitada para PolyBase autônoma.  
   
     Escolha essa opção para usar a instância do SQL Server como um nó de cabeçalho autônomo.  
   
   - Use a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase. Essa opção abre o firewall para permitir conexões de entrada. As conexões são permitidas para o Mecanismo de Banco de Dados do SQL Server, o Mecanismo PolyBase do SQL Server, o serviço de Movimentação de Dados PolyBase do SQL Server e o SQL Browser. O firewall também permite conexões de entrada de outros nós em um grupo de escala horizontal do PolyBase.  
   
     Esta opção também habilita conexões de firewall do MSDTC (Coordenador de Transações Distribuídas da Microsoft) e modifica as configurações de Registro do MSDTC.  
   
6. Na página de Configuração do PolyBase, especifique um intervalo de portas com pelo menos seis portas. A instalação do SQL Server aloca as primeiras seis portas disponíveis do intervalo.  

   >[!IMPORTANT]
   > Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).


##  <a name="installing"></a> Use um prompt de comando

Use os valores nesta tabela para criar scripts de instalação. Os serviços de Mecanismo PolyBase do SQL Server e de Movimentação de Dados PolyBase do SQL Server devem ser executados na mesma conta. Em um grupo de escala horizontal do PolyBase, os serviços do PolyBase em todos os nós devem ser executados na mesma conta de domínio.  
   
<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017"

|Componente do SQL Server|Parâmetro e valores|Descrição|  
|--------------------------|--------------------------|-----------------|  
|Controle de instalação do SQL Server|**Required**<br /><br /> /FEATURES=PolyBase|Seleciona o recurso PolyBase.|  
|Mecanismo de PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCACCOUNT|Especifica a conta do serviço de mecanismo. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCPASSWORD|Especifica a senha da conta de serviço de mecanismo.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCSTARTUPTYPE|Especifica o modo de inicialização para o Mecanismo PolyBase: Automático (padrão), Desabilitado e Manual.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCACCOUNT|Especifica a conta do serviço de movimentação de dados. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCPASSWORD|Especifica a senha para a conta de movimentação de dados.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Especifica o modo de inicialização do serviço de movimentação de dados: Automático (padrão), Desabilitado e Manual.|  
|PolyBase|**Opcional**<br /><br /> /PBSCALEOUT|Especifica se a instância do SQL Server é usada como parte do grupo computacional de escala horizontal do PolyBase. <br />Valores com suporte: Verdadeiro, Falso.|  
|PolyBase|**Opcional**<br /><br /> /PBPORTRANGE|Especifica um intervalo de portas com pelo menos seis portas para serviços do PolyBase. Exemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

|Componente do SQL Server|Parâmetro e valores|Descrição|  
|--------------------------|--------------------------|-----------------|  
|Controle de instalação do SQL Server|**Necessário**<br /><br /> /FEATURES=PolyBaseCore, PolyBaseJava, PolyBase | O PolyBaseCore instala o suporte para todos os recursos do PolyBase, exceto a conectividade do Hadoop. O PolyBaseJava habilita a conectividade do Hadoop. O PolyBase instala ambos. |  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCACCOUNT|Especifica a conta do serviço de mecanismo. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCPASSWORD|Especifica a senha da conta de serviço de mecanismo.|  
|Mecanismo PolyBase do SQL Server|**Opcional**<br /><br /> /PBENGSVCSTARTUPTYPE|Especifica o modo de inicialização para o Mecanismo PolyBase: Automático (padrão), Desabilitado e Manual.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCACCOUNT|Especifica a conta do serviço de movimentação de dados. O padrão é **NT Authority\NETWORK SERVICE**.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCPASSWORD|Especifica a senha para a conta de movimentação de dados.|  
|Movimentação de Dados PolyBase do SQL Server |**Opcional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Especifica o modo de inicialização do serviço de movimentação de dados: Automático (padrão), Desabilitado e Manual.|  
|PolyBase|**Opcional**<br /><br /> /PBSCALEOUT|Especifica se a instância do SQL Server é usada como parte do grupo computacional de escala horizontal do PolyBase. <br />Valores com suporte: Verdadeiro, Falso.|  
|PolyBase|**Opcional**<br /><br /> /PBPORTRANGE|Especifica um intervalo de portas com pelo menos seis portas para serviços do PolyBase. Exemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end

Após a instalação, é necessário [habilitar o recurso do PolyBase](#enable).



**Exemplo**

Este exemplo exibe uma amostra de script de instalação.  

```cmd
   
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,PolyBase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
   
```  

## <a id="enable"></a> Habilitar o PolyBase

Após a instalação, o PolyBase deverá ser habilitado para acessar seus recursos. Use o seguinte comando Transact-SQL. As instâncias do SQL 2019 implantadas durante a instalação do cluster de Big Data têm essa configuração habilitada por padrão.


```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE;
```


## <a name="post-installation-notes"></a>Notas de pós-instalação  

O PolyBase instala três bancos de dados de usuário: DWConfiguration, DWDiagnostics e DWQueue. Esses bancos de dados são para uso do PolyBase. Não os altere ou exclua.  
   
### <a id="confirminstall"></a> Como confirmar a instalação  

Execute o comando a seguir. Se o PolyBase estiver instalado, o retorno será 1. Caso contrário, é 0.  

```sql  
SELECT SERVERPROPERTY ('IsPolyBaseInstalled') AS IsPolyBaseInstalled;  
```  

### <a name="firewall-rules"></a>Regras de firewall  

A instalação do PolyBase do SQL Server cria as seguintes regras de firewall no computador:  
   
- PolyBase do SQL Server – Mecanismo de Banco de Dados – \<SQLServerInstanceName> (TCP-In)  
   
- PolyBase do SQL Server – Serviços do PolyBase – \<SQLServerInstanceName> (TCP-In)  

- PolyBase do SQL Server – Navegador do SQL – (UDP-In)  
   
Durante a instalação, se você usar a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase, essas regras serão habilitadas. O firewall abre e permite conexões de entrada. São permitidas para o Mecanismo de Banco de Dados do SQL Server, o Mecanismo PolyBase do SQL Server, o serviço de Movimentação de Dados PolyBase do SQL Server e o SQL Browser. Se o serviço de firewall no computador não estiver em execução durante a instalação, a instalação do SQL Server falhará ao habilitar essas regras. Nesse caso, inicie o serviço de Firewall no computador e habilite essas regras pós-instalação.  
   
#### <a name="to-enable-the-firewall-rules"></a>Para habilitar as regras de firewall  

1. Abra o **Painel de Controle**.  

2. Selecione **Sistema e Segurança** e depois **Firewall do Windows**.  
   
3. Selecione **Configurações Avançadas**e **Regras de entrada**.  
   
4. Clique com o botão direito do mouse na regra desabilitada e depois selecione **Habilitar regra**.  
   
### <a name="polybase-service-accounts"></a>Contas de serviço do PolyBase

Para alterar as contas de serviço para os serviços de Mecanismo de PolyBase e de Movimentação de Dados do PolyBase, desinstale e reinstale o recurso PolyBase.

## <a name="next-steps"></a>Próximas etapas  

Veja [Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md).
