---
title: Especificação de Backup de VDI – SQL Server no Linux | Microsoft Docs
description: Especificação de Interface de dispositivo Virtual de Backup do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: f417002cc3a778b0406cc56e763b8d7b4931b0c6
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660136"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server no cliente Linux VDI especificação de SDK

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento aborda as interfaces fornecidas pelo SQL Server no SDK de cliente de interface (VDI) de dispositivo virtual do Linux. Fornecedores de software independentes (ISVs) podem usar o Virtual Backup dispositivo aplicativo Interface de programação (API) para integrar o SQL Server em seus produtos. Em geral, VDI no Linux se comporta da mesma forma para VDI no Windows com as seguintes alterações:

- Memória compartilhada do Windows se torna a memória compartilhada do POSIX.
- Windows semáforos se tornar semáforos POSIX.
- Tipos de Windows como DWORD e HRESULT são alterados para os equivalentes de inteiro.
- As interfaces COM são removidas e substituídas com um par de Classes do C++.
- SQL Server no Linux não oferece suporte a instâncias nomeadas, para que as referências ao nome da instância foram removidas. 
- A biblioteca compartilhada é implementada no libsqlvdi.so instalados em /opt/mssql/lib/libsqlvdi.so

Este documento é um adendo ao **vbackup.chm** que fornece detalhes sobre a especificação de VDI do Windows. Baixe o [especificação de VDI Windows](https://www.microsoft.com/download/details.aspx?id=17282).

Revise também a solução de backup de VDI de exemplo na [repositório GitHub de exemplos do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Configuração de permissões de usuário

No Linux, primitivos POSIX são pertencentes ao usuário que criar esses aplicativos e seus grupos padrão. Para objetos criados pelo SQL Server, eles serão por padrão de propriedade ao usuário mssql e o grupo de mssql. Para permitir o compartilhamento entre o SQL Server e o cliente VDI, um dos dois métodos a seguir são recomendadas:

1. Executar o cliente de VDI como o usuário mssql
   
   Execute o seguinte comando para alternar para o usuário mssql:
   
   ```bash
   sudo su mssql
   ```

2. Adicione o usuário mssql ao grupo do vdiuser e o vdiuser ao grupo mssql.
   
   Execute os seguintes comandos:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Reinicie o servidor para acompanhar os novos grupos do SQL Server e vdiuser

## <a name="client-functions"></a>Funções do cliente

Este capítulo contém descrições de cada uma das funções de cliente. As descrições incluem as seguintes informações:

- Finalidade da função
- Sintaxe de função
- lista de parâmetros
- Valores retornados
- Comentários

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**Finalidade** essa função cria o conjunto de dispositivo virtual.

**Sintaxe**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **name** | Isso identifica o conjunto de dispositivo virtual. As regras para nomes usados pelo CreateFileMapping () devem ser seguidas. Qualquer caractere, exceto a barra invertida (\) pode ser usado. Isso é uma cadeia de caracteres. É recomendável prefixando a cadeia de caracteres com o nome do produto ou da empresa e o nome do banco de dados do usuário. |
| |**cfg** | Essa é a configuração para o conjunto de dispositivo virtual. Para obter mais informações, consulte "Configuração" neste documento.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** | A função foi bem-sucedida. |
| |**VD_E_NOTSUPPORTED** |Um ou mais dos campos na configuração era inválido ou não compatível. |
| |**VD_E_PROTOCOL** | O dispositivo virtual definido já existe.

**Comentários** criar o método deve ser chamado apenas uma vez por operação de BACKUP ou restauração. Depois de invocar o método Close, o cliente pode reutilizar a interface para criar outro conjunto de dispositivo virtual.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Finalidade** essa função é usada para aguardar o servidor configurar o conjunto de dispositivo virtual.
**Sintaxe**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **timeout** | Esse é o tempo limite em milissegundos. Use infinito ou qualquer inteiro negativo para evitar o tempo limite.
| | **cfg** | Após a execução bem-sucedida, contém a configuração selecionada pelo servidor. Para obter mais informações, consulte "Configuração" neste documento.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** | A configuração foi retornada.
| |**VD_E_ABORT** |SignalAbort foi invocado.
| |**VD_E_TIMEOUT** |A função atingiu o tempo limite.

**Comentários** essa função bloqueia em um estado de alerta. Após uma chamada bem-sucedida, os dispositivos no conjunto de dispositivo virtual podem ser abertos.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Finalidade** essa função é aberto um dos dispositivos no conjunto de dispositivo virtual.
**Sintaxe**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **name** |Isso identifica o conjunto de dispositivo virtual.
| | **ppVirtualDevice** |Quando a função for bem-sucedida, um ponteiro para o dispositivo virtual é retornado. Este dispositivo é usado para GetCommand e CompleteCommand.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_ABORT** | Anulação foi solicitada.
| |**VD_E_OPEN** |  Todos os dispositivos estão abertos.
| |**VD_E_PROTOCOL** |  O conjunto não está no estado inicializando ou esse dispositivo em particular já está aberto.
| |**VD_E_INVALID** |O nome do dispositivo é inválido. Não é um dos nomes conhecidos que compõem o conjunto.

**Comentários** VD_E_OPEN podem ser retornados sem problema. O cliente pode chamar OpenDevice por meio de um loop até que esse código é retornado.
Se mais de um dispositivo estiver configurado, por exemplo *n* dispositivos, o conjunto de dispositivo virtual retornará *n* interfaces de dispositivo exclusivo.

O `GetConfiguration` função pode ser usada para aguardar até que os dispositivos podem ser abertos.
Se essa função não for bem-sucedida, um valor nulo é retornado por meio de ppVirtualDevice.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Finalidade** essa função é usada para obter o próximo comando na fila para um dispositivo. Quando solicitado, essa função aguarda o próximo comando.

**Sintaxe**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**timeout** |Isso é o tempo de espera, em milissegundos. Use FINITA para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando está disponível no momento. Se o tempo limite ocorrer, o cliente decide a próxima ação.
| |**Tempo Limite** |Isso é o tempo de espera, em milissegundos. Use FINITA ou um valor negativo para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando está disponível antes do tempo limite expirar. Se o tempo limite ocorrer, o cliente decide a próxima ação.
| |**ppCmd** |Quando um comando é retornado com êxito, o parâmetro retorna o endereço de um comando seja executado. A memória retornada é somente leitura. Quando o comando for concluído, esse ponteiro é passado para a rotina CompleteCommand. Para obter detalhes sobre cada comando, consulte "Comandos" neste documento.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Um comando foi buscado.
| |**VD_E_CLOSE** |O dispositivo foi fechado pelo servidor.
| |**VD_E_TIMEOUT** |Nenhum comando estava disponível e o tempo limite expirou.
| |**VD_E_ABORT** |O cliente ou o servidor tem usado o SignalAbort para forçar o desligamento.

**Comentários** VD_E_CLOSE quando é retornado, o SQL Server encerrou o dispositivo. Isso faz parte do desligamento normal. Depois que todos os dispositivos foram fechados, o cliente invoca ClientVirtualDeviceSet::Close para fechar o conjunto de dispositivo virtual.
Quando essa rotina deve bloquear a espera para um comando, o thread será deixado em uma condição de alerta.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Finalidade** essa função é usada para notificar o SQL Server que um comando foi concluído. Informações de conclusão apropriadas para o comando devem ser retornadas. Para obter mais informações, consulte "Comandos" neste documento.

**Sintaxe** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**pCmd** |Esse é o endereço de um comando retornado anteriormente de ClientVirtualDevice::GetCommand.
| |**completionCode** |Este é um código de status que indica o status de conclusão. Esse parâmetro deve ser retornado para todos os comandos. O código retornado deve ser apropriado para o comando que está sendo executado. ERROR_SUCCESS é usado em todos os casos, a fim de denotar um comando executado com êxito. Para obter uma lista dos possíveis códigos, consulte o arquivo, vdierror.h. Uma lista típica de códigos de status para cada comando aparece no "Commands" neste documento.
| |**bytesTransferred** |Isso é o número de bytes transferidos com êxito. Isso é retornado apenas para a transferência de dados, comandos de leitura e gravação.
| |**position** |Esta é uma resposta ao comando GetPosition apenas.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Após a conclusão foi observada corretamente.
| |**VD_E_INVALID** |pCmd não era um comando do Active Directory.
| |**VD_E_ABORT** |Anulação foi sinalizada.
| |**VD_E_PROTOCOL** |O dispositivo não está aberto.

**Comentários** None

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Finalidade** essa função é usada para sinalizar que um encerramento anormal deve ocorrer.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |None | Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR**|A notificação de anulação foi lançada com êxito.

**Comentários** a qualquer momento, o cliente pode optar por anular a operação de BACKUP ou restauração. Essa rotina sinaliza que devem encerrar a todas as operações. O estado do conjunto de dispositivo virtual geral entra em um estado de encerrado de maneira anormal. Nenhum comando adicional é retornado em qualquer dispositivo. Todos os comandos não concluídos são concluídos automaticamente, retornando ERROR_OPERATION_ABORTED como um código de conclusão. O cliente deve chamar ClientVirtualDeviceSet::Close depois que ele foi finalizado com segurança qualquer uso pendente de buffers fornecido ao cliente. Para obter mais informações, consulte "Um encerramento anormal" no início deste documento.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Finalidade** essa função fecha o conjunto de dispositivo virtual criado pela ClientVirtualDeviceSet::Create. Isso resulta na versão de todos os recursos associados com o conjunto de dispositivo virtual.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |None |Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Isso é retornado quando o conjunto de dispositivo virtual foi fechado com êxito.
| |**VD_E_PROTOCOL** |Nenhuma ação foi executada porque o conjunto de dispositivo virtual não foi aberto.
| |**VD_E_OPEN** |Dispositivos ainda estavam abertos.

**Comentários** a invocação do fechamento é uma declaração de cliente que todos os recursos usados pelo conjunto de dispositivo virtual devem ser liberados. O cliente deve garantir que todas as atividades que envolvem os buffers de dados e dispositivos virtuais é encerrada antes de invocar a fechar. Todas as interfaces de dispositivo virtual retornadas pela OpenDevice serão invalidadas por perto.
O cliente tenha permissão para emitir uma chamada de criação na interface de conjunto de dispositivo virtual depois que a chamada de fechamento é retornado. Essa chamada criaria um novo dispositivo virtual definido para uma operação de BACKUP ou RESTORE subsequente.
Se fechar é chamado quando um ou mais dispositivos virtuais ainda estão abertos, VD_E_OPEN será retornado. Nesse caso, SignalAbort é internamente disparado, para garantir um desligamento correto se possível. Recursos VDI são liberados. O cliente deve esperar para ter uma indicação de VD_E_CLOSE em cada dispositivo antes de invocar ClientVirtualDeviceSet::Close. Se o cliente sabe que o conjunto de dispositivo virtual já está em um estado de encerrado de maneira anormal, em seguida, ele não deve esperar que uma indicação de VD_E_CLOSE de GetCommand e pode invocar ClientVirtualDeviceSet::Close assim que a atividade em buffers compartilhados será encerrada.
Para obter mais informações, consulte "Um encerramento anormal" no início deste documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Finalidade** essa função abre o dispositivo virtual definido em um cliente secundário. O cliente primário deve ter já usado criar e GetConfiguration para configurar o conjunto de dispositivo virtual.

**Sintaxe** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**setName** |Isso identifica o conjunto. Esse nome diferencia maiusculas de minúsculas e deve corresponder ao nome usado pelo cliente primário quando invocada ClientVirtualDeviceSet::Create.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não tiver sido criado, já foi aberto nesse cliente ou o dispositivo virtual conjunto não está pronto para aceitar solicitações abertas de clientes secundários.
| |**VD_E_ABORT** |A operação está sendo anulada.

**Comentários** ao usar um modelo de processo múltiplo, o cliente primário é responsável por detectar o encerramento normal e anormal de clientes secundários.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Finalidade** alguns aplicativos podem exigir mais de um processo para operar em buffers retornados por ClientVirtualDevice::GetCommand. Nesses casos, o processo que recebe o comando pode usar GetBufferHandle para obter um identificador de processo independente que identifica o buffer. Esse identificador, em seguida, poderá ser comunicada ao outro processo que também tem de abrir o mesmo conjunto de dispositivo Virtual. Esse processo, em seguida, usaria ClientVirtualDeviceSet::MapBufferHandle para obter o endereço do buffer. O endereço provavelmente será um endereço diferente em seu parceiro, porque cada processo pode ser mapeando buffers em endereços diferentes.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**pBuffer** |Esse é o endereço de um buffer obtido de um comando de leitura ou gravação.
| |**BufferHandle** |Um identificador exclusivo para o buffer é retornado.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não está aberto atualmente.
| |**VD_E_INVALID** |O pBuffer não é um endereço válido.
Comentários do processo que invoca a função GetBufferHandle é responsável por invocar ClientVirtualDevice::CompleteCommand quando a transferência de dados for concluída.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Finalidade** essa função é usada para obter um endereço do buffer válido de um identificador do buffer obtido de algum outro processo. 

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**dwBuffer** |Isso é o identificador retornado por ClientVirtualDeviceSet::GetBufferHandle.
| |**ppBuffer** |Esse é o endereço do buffer que é válido no processo atual.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não está aberto atualmente.
| |**VD_E_INVALID** |O ppBuffer é um identificador inválido.

**Comentários** é necessário ter cuidado para comunicar as alças corretamente. Os identificadores são locais para um conjunto único de dispositivo virtual. Os processos de parceiro, um identificador de compartilhamento devem garantir que esse buffer identificadores são usados somente dentro do escopo do dispositivo virtual definido do qual o buffer foi originalmente definido.


