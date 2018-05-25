---
title: Especificação de Backup VDI - SQL Server no Linux | Microsoft Docs
description: Especificação de Interface de dispositivo Virtual de Backup do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: 1dab0dcc403a7e0f85cd78e69e9461ef0d566b0c
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server no cliente do Linux VDI especificação do SDK

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento aborda as interfaces fornecidas pelo SQL Server no SDK de cliente de interface (VDI) de dispositivo virtual do Linux. Fornecedores de software independentes (ISVs) podem usar o Virtual Backup dispositivo aplicativo Interface de programação (API) para integrar o SQL Server em seus produtos. Em geral, VDI no Linux se comporta da mesma forma para VDI no Windows com as seguintes alterações:

- Memória compartilhada do Windows se torna a memória compartilhada de POSIX.
- Windows semáforos se tornar POSIX semáforos.
- Tipos de Windows como HRESULT e DWORD são alterados para os equivalentes de inteiro.
- As interfaces COM são removidas e substituídas por um par de Classes C++.
- SQL Server no Linux não oferece suporte a instâncias nomeadas para que referências ao nome da instância foram removidas. 
- A biblioteca compartilhada é implementada no libsqlvdi.so instalado em /opt/mssql/lib/libsqlvdi.so

Este documento é um adendo a **vbackup.chm** que fornece detalhes sobre a especificação de VDI do Windows. Baixe o [Windows VDI especificação](http://www.microsoft.com/download/details.aspx?id=17282).

Examine também o exemplo de solução de backup de VDI no [repositório GitHub de exemplos do SQL Server](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Configuração de permissões do usuário

No Linux, primitivos POSIX são de propriedade do usuário criando-los e seus grupos padrão. Para objetos criados pelo SQL Server, esses serão por padrão de propriedade pelo usuário mssql e o grupo mssql. Para permitir o compartilhamento entre o SQL Server e o cliente VDI, um dos dois métodos a seguir são recomendadas:

1. Execute o cliente de VDI como o usuário mssql
   
   Execute o seguinte comando para alternar para o usuário mssql:
   
   ```bash
   sudo su mssql
   ```

2. Adicione o usuário de mssql ao grupo do vdiuser e vdiuser ao grupo mssql.
   
   Execute os seguintes comandos:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Reinicie o servidor para acompanhar os novos grupos do SQL Server e vdiuser

## <a name="client-functions"></a>Funções de cliente

Este capítulo contém descrições de cada uma das funções de cliente. As descrições incluem as seguintes informações:

- Finalidade de função
- Sintaxe de função
- Lista de parâmetros
- Valores retornados
- Remarks

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
| |**cfg** | Essa é a configuração para o conjunto de dispositivo virtual. Para obter mais informações, consulte "Configuração", posteriormente neste documento.

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
| | **timeout** | Este é o tempo limite em milissegundos. Use INFINITAS ou qualquer inteiro negativo para impedir que o tempo limite.
| | **cfg** | Após a execução bem-sucedida, contém a configuração selecionada pelo servidor. Para obter mais informações, consulte "Configuração", posteriormente neste documento.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** | A configuração foi retornada.
| |**VD_E_ABORT** |SignalAbort foi invocado.
| |**VD_E_TIMEOUT** |A função atingiu o tempo limite.

**Comentários** essa função blocos em um estado de alerta. Após a chamada bem-sucedida, os dispositivos no conjunto de dispositivo virtual podem ser abertos.


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
| | **ppVirtualDevice** |Quando a função tiver êxito, será retornado um ponteiro para o dispositivo virtual. Este dispositivo é usado para GetCommand e CompleteCommand.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_ABORT** | Anulação foi solicitada.
| |**VD_E_OPEN** |  Todos os dispositivos estão abertos.
| |**VD_E_PROTOCOL** |  O conjunto não está no estado inicializando ou esse dispositivo em particular já está aberto.
| |**VD_E_INVALID** |O nome do dispositivo é inválido. Não é um dos nomes de conhecido que compõem o conjunto.

**Comentários** VD_E_OPEN podem ser retornados sem problema. O cliente pode chamar OpenDevice por meio de um loop até que este código é retornado.
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
| |**timeout** |Este é o tempo de espera em milissegundos. Use INFINTE para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando está disponível no momento. Se o tempo limite ocorrer, o cliente decide a próxima ação.
| |**Tempo Limite** |Este é o tempo de espera em milissegundos. Use INFINTE ou um valor negativo para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando está disponível antes do tempo limite expirar. Se o tempo limite ocorrer, o cliente decide a próxima ação.
| |**ppCmd** |Quando um comando é retornado com êxito, o parâmetro retorna o endereço de um comando seja executado. A memória retornada é somente leitura. Quando o comando for concluído, esse ponteiro é passado para a rotina CompleteCommand. Para obter detalhes sobre cada comando, consulte "Comandos", posteriormente neste documento.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Um comando foi encontrado.
| |**VD_E_CLOSE** |O dispositivo foi fechado pelo servidor.
| |**VD_E_TIMEOUT** |Nenhum comando estava disponível e o tempo limite expirou.
| |**VD_E_ABORT** |O cliente ou servidor usou o SignalAbort para forçar o desligamento.

**Comentários** VD_E_CLOSE quando é retornado, o SQL Server encerrou o dispositivo. Isso faz parte do desligamento normal. Depois que todos os dispositivos foram fechados, o cliente chama ClientVirtualDeviceSet::Close para fechar o conjunto de dispositivo virtual.
Quando esta rotina deve bloquear a esperar para um comando, o thread será deixado em uma condição de alerta.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Finalidade** essa função é usada para notificar o SQL Server que um comando terminou. Informações de conclusão apropriadas para o comando devem ser retornadas. Para obter mais informações, consulte "Comandos", posteriormente neste documento.

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
| |**pCmd** |Este é o endereço de um comando anteriormente retornado de ClientVirtualDevice::GetCommand.
| |**completionCode** |Este é um código de status que indica o status de conclusão. Esse parâmetro deve ser retornado para todos os comandos. O código retornado deve ser apropriado para o comando que está sendo executado. ERROR_SUCCESS é usado em todos os casos para denotar um comando executado com êxito. Para obter uma lista de possíveis códigos, consulte o arquivo vdierror.h. Aparece uma lista de códigos de status típicos para cada comando em "Comandos" neste documento.
| |**bytesTransferred** |Este é o número de bytes transferidos com êxito. Isso será retornado apenas para a transferência de dados, comandos de leitura e gravação.
| |**position** |Esta é uma resposta para o comando GetPosition somente.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A conclusão foi observada corretamente.
| |**VD_E_INVALID** |pCmd não era um comando ativo.
| |**VD_E_ABORT** |Anular foi sinalizado.
| |**VD_E_PROTOCOL** |O dispositivo não está aberto.

**Comentários** None

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Finalidade** essa função é usada para sinalizar que ocorra um encerramento anormal.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |Nenhuma | Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR**|A notificação de anulação foi lançada com êxito.

**Comentários** a qualquer momento, o cliente pode optar por cancelar a operação de BACKUP ou restauração. Esta rotina indica que todas as operações devem cessar. O estado do conjunto de dispositivo virtual geral entra em um estado terminada de maneira anormal. Não há comandos adicionais serão retornados todos os dispositivos. Todos os comandos não concluídos são concluídos automaticamente, retornando ERROR_OPERATION_ABORTED como um código de conclusão. O cliente deve chamar ClientVirtualDeviceSet::Close depois que ele foi encerrado com segurança qualquer uso pendente de buffers fornecido ao cliente. Para obter mais informações, consulte "Encerramento anormal", anteriormente neste documento.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Finalidade** essa função fecha o conjunto de dispositivo virtual criado pelo ClientVirtualDeviceSet::Create. Isso resulta na versão de todos os recursos associados com o conjunto de dispositivo virtual.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |Nenhuma |Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Isso é retornado quando o conjunto de dispositivo virtual foi fechado com êxito.
| |**VD_E_PROTOCOL** |Nenhuma ação foi executada porque o conjunto de dispositivo virtual não foi aberto.
| |**VD_E_OPEN** |Dispositivos foram abertos.

**Comentários** a invocação de fechamento é uma declaração de cliente que todos os recursos usados pelo conjunto de dispositivo virtual devem ser liberados. O cliente deve garantir que todas as atividades envolvendo buffers de dados e dispositivos virtuais é encerrada antes de chamar fechar. Todas as interfaces de dispositivo virtual retornadas por OpenDevice são invalidadas pelo fechamento.
O cliente tem permissão para emitir uma chamada de criação na interface de conjunto de dispositivo virtual depois que a chamada de fechamento é retornado. Essa chamada criaria um novo dispositivo virtual definido para uma operação de BACKUP ou restauração subsequente.
Se fechar é chamado quando um ou mais dispositivos virtuais ainda estão abertos, VD_E_OPEN será retornado. Nesse caso, SignalAbort é internamente disparado, para garantir um desligamento correto se possível. VDI recursos são liberados. O cliente deve esperar para uma indicação de VD_E_CLOSE em cada dispositivo antes de chamar ClientVirtualDeviceSet::Close. Se o cliente sabe que o conjunto de dispositivo virtual já está em um estado terminada de maneira anormal, ele não deve esperar uma indicação de VD_E_CLOSE de GetCommand e pode invocar ClientVirtualDeviceSet::Close assim que a atividade em buffers compartilhados é encerrada.
Para obter mais informações, consulte "Encerramento anormal", anteriormente neste documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Finalidade** essa função abre o dispositivo virtual definido em um cliente secundário. O cliente primário deve já ter usado criar e GetConfiguration para configurar o conjunto de dispositivo virtual.

**Sintaxe** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**setName** |Isso identifica o conjunto. Esse nome diferencia maiusculas de minúsculas e deve corresponder ao nome usado pelo cliente primário quando chamada ClientVirtualDeviceSet::Create.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não foi criado, já foi aberta no cliente ou o dispositivo virtual conjunto não está pronto para aceitar solicitações abertas de clientes secundários.
| |**VD_E_ABORT** |A operação está sendo anulada.

**Comentários** ao usar um modelo de processo múltiplo, o cliente primário é responsável por detectar um encerramento normal e anormal de clientes secundários.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Finalidade** alguns aplicativos podem exigir mais de um processo para operar em buffers retornados por ClientVirtualDevice::GetCommand. Nesses casos, o processo que recebe o comando pode usar GetBufferHandle para obter um identificador de processo independente que identifica o buffer. Esse identificador, em seguida, pode ser comunicada ao outro processo que também tenha o mesmo aberto do dispositivo Virtual definido. Esse processo, em seguida, usaria ClientVirtualDeviceSet::MapBufferHandle para obter o endereço do buffer. O endereço provavelmente será um endereço diferente do seu parceiro porque cada processo pode ser mapeamento buffers em endereços diferentes.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**pBuffer** |Este é o endereço de um buffer obtido de um comando de leitura ou gravação.
| |**BufferHandle** |Um identificador exclusivo para o buffer é retornado.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não está aberto atualmente.
| |**VD_E_INVALID** |O pBuffer não é um endereço válido.
Comentários do processo que invoca a função GetBufferHandle é responsável por invocar ClientVirtualDevice::CompleteCommand quando a transferência de dados for concluída.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Finalidade** essa função é usada para obter um endereço válido de buffer de um identificador de buffer obtido de algum outro processo. 

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**dwBuffer** |Este é o identificador retornado por ClientVirtualDeviceSet::GetBufferHandle.
| |**ppBuffer** |Este é o endereço do buffer que é válido no processo atual.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivo virtual não está aberto atualmente.
| |**VD_E_INVALID** |O ppBuffer é um identificador inválido.

**Comentários** deve ter cuidado para comunicar as alças corretamente. Identificadores são locais para um conjunto único de dispositivo virtual. Os processos de parceiro, um identificador de compartilhamento devem garantir que buffer identificadores são usados somente dentro do escopo do dispositivo virtual definido do que o buffer foi originalmente obtido.


