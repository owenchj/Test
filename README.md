# Verilog Format
```verilog
// -----------------------------------------------------------------------------
// Module Name: s26ks512s.v
// -----------------------------------------------------------------------------
// Copyright (C) 2015 - 2021 GreenWave Technologies, Inc.
// -----------------------------------------------------------------------------
//
// PART DESCRIPTION:
//
// Library:        --
// Technology:     --
// Part:           --
//
// Description:   RPC - Reduced Pin Count Flash Memory,
//                 512Mb (64MByte) CMOS 1.8 Volt Core and I/O,
//                 MirrorBit NOR flash Technology, x8 data bus
//
// -----------------------------------------------------------------------------
// Department: Shanghai R&D Center
// -----------------------------------------------------------------------------
// MODIFICATION HISTORY :
//
//  version:  | author:        |   date:    | changes made:
//    V1.0     R.Prokopovic     13 Apr 30     Initial release
//
//    V1.1     R. Prokopovic    13 May 15   Improved read operation for
//                                          different ASOs, fixed sector
//                                          Protection, fixed ASPR register
//                                          programming, FSM state transitions,
//                                         fixed Buffer programming of SSR ASO
//    V1.2     R. Prokopovic    13 May 23  Device times, scaled values, updated
//                                         Program operation time for single
//                                         word and page program is updated,
//                                         now it is the same time tdevice_SWPB
//    V1.3     R. Prokopovic    13 Jun 4   Burst Write feature added
//                                         CRC read states updated
//                                         Protection condition of DYB fixed,
//                                         ASPR_reg[0] only for PPB
//                                         Programming of ASPR_reg[2:1] with
//                                        2'b11 is not allowed
//    V1.4     R. Prokopovic    13 Jun 10 Program Error state fixed
//                                        Program and Erase protection fixed
//                                        Read of Suspended Line fixed
//                                        Burst Length read fixed
//                                        Program of ASP register fixed
//
//    V1.5    R.Prokopovic     13 Jul 01    Password program update, forbid
//                                          password program when ASPR[2] is 0
//                                          Set program fail bit and sector
//                                          lock bit when wrong password is
//                                          is provided
//    V1.6    R.Prokopovic      13 Sep 02  Warning message for burst write fix
//                                       SSR buffer program region address fix
//                                       Corrupt lines uses WBLine instead of
//                                       WLine variable
//                                       Flags added for program and erase due
//                                       to errors when 2 triggers occur in one
//                                       program or erase state
//    V1.7    S.Petrovic        14 Feb 14 Update to datasheet S80KS Rev0.63.pdf
//    V1.8    S.Petrovic        14 Feb 20 Corrected burst read implementation
//    V1.9    S.Petrovic        14 Feb 21 Corrected chip and sector erase
//                                        implementation
//    V1.10   S.Petrovic        14 Mar 20 CRC calculation corrected;
//                                        Write to lowest 16 bytes of SSR enabled;
//                                        Sector protect status corrected
//    V1.11   S.Petrovic        14 Mar 21 CRC calculation corrected
//    V1.12   S.Petrovic        14 Mar 25 Corrected bug in LRPG1 state
//    V1.13   S.Petrovic        14 Apr 11 Read burst corrected
//    V1.14   I.Viljacik        14 May 27 Update to datasheet S26KS_032S_02GT
//    V1.15   S.Petrovic        14 May 29 Corrected sensitivity list of
//                                        Functional block.
//    V1.16   S.Petrovic        14 Jun 03 Update to datasheet Rev0.79
//    V1.17   S.Petrovic        14 Jun 05 Corrected CFI array
//    V1.18   S.Stevanovic      15 Jul 21   Update to HBP_DRS_2_150508.pdf with
//                                          supplement documents
//                                          Fixed DPD exit condition, setting
//                                          default values after exiting DPD.
//                                          Hybrid Burst Enable fixed.
//                                          64B Wrapped Burst fixed.
//    V1.19   S.Stevanovic      15 Jul 31   tACC time checking fixed
//    V1.20   M.Stojanovic      15 Oct 14   POR & RESET# issue (bug #491) fixed
//    V1.21   M.Stojanovic      15 Nov 09  Changed name from "BUFFER" to "BUFFERs26ks512s"
//                                         (bug #492 fixed)
//    V1.22   S.Stevanovic      16 Jan 27   #493 and #495 fixed. In ESUL2,
//                                          ESPSULS2, and PSUL2 states for 88h
//                                          command check (SA) 555h instead of
//                                          (SA) 55h
//    V1.23   M.Stojanovic      16 Mar 14  #504 fixed - secure region
//    V1.24   M.Stojanovic      16 Oct 10  RWDS doesn't depends on the CLK edge (#515 fixed)
//    V1.25   M.Stojanovic      17 Feb 18  Fixing for loops for WBData and WBAddr in ESPG,
//                                         ESPSR, PG, PSR, LRPG. Loops should count from
//                                         (wr_cnt - 1).
//
//
// -----------------------------------------------------------------------------
// Comments: For correct simulation, simulator resolution should be set to 1 ps
//
// -----------------------------------------------------------------------------
// Known Bugs:
//
// -----------------------------------------------------------------------------

// -----------------------------------------------------------------------------
// MODULE EXAMPLE
// -----------------------------------------------------------------------------
module counter
    (
     // Clock and resetn
     input        clk_i,
     input        rstn_i,

     // Configuration signals
     input        cfg_start_i, // FP (false path)
     input [3:0]  cfg_init_value_i, // MP2 (multicycle path of 2 cycles)

     // Bus/FIFO signal
     // ...

     // Output signals
     output       valid_o,
     output [3:0] result_o
     );

    // Net, replace digital to meaningful signals
    wire          s_0;

    // Register, replace digital to meaningful signals
    reg [3:0]     r_0;
    reg           r_valid;

    // Assign output signals
    assign result_o = r_0;
    assign valid_o  = r_valid;

    // Assign temp signals
    assign s_0 = (r_0 >= 4'h8) ? 1'b1 : 1'b0;

    always @(posedge clk_i or negedge rstn_i)
        begin
            if (~rstn_i) begin
                r_0     <= 4'h0;
                r_valid <= 1'b1;
            end else begin
                if (s_0)
                    r_valid <= 1'b1;
                else
                    r_valid <= 1'b0;

                if (cfg_start_i) begin
                    r_0 <= cfg_init_value_i;
                end else begin
                    r_0 <= r_0 + 1;
                end
            end
        end

endmodule
```


# Rules
## 格式规则
 - 规则1: 行首用Tab键对齐，Tab键的宽度设为4，在最终递交代码时，由工具统一将其自动转换为空格。有条件作者可直接设置编辑器为4空格对齐。
- 规则2：Verilog HDL 关键字与其他字符串之间保留有一个空格，如：

```verilog
    always@ (......)
    if (......)
    assign a = b + c;
    b <= a && c;
```

- 规则3：单目运算符与变量之间不留空格，如：a = ( ~b );
- 规则4：begin_end 按照如下规范进行规范：

```verilog
    always@ (posedge clk_i or negedge rstn_i) begin
        if (~rstn_i)
            a <= 1'b0;
        else if (...)
        else begin
            if (...)
                a <= a + 1;
            else
                a <= a - 1;
        end
    end
```
- 规则5：使用括号表示运算优先级。
- 规则6：一行中不能出现多个表达式。
- 规则7：设计中使用到的0 1 z 等常数采用基数表示法书写 （即表示为 1'b0, 1'b1, 1'bz 或十六进制 4'h0, 4'h5, 16'h1234）。

## 命名规则
 - 规则1：模块的命名规则：首字母使用除字母“u”以外的字母，最多只能在中间使用一个“_”字符，数字只能表示数据位宽，如：LTE_crc7 counter my_spi
 - 规则2: 模块实例化的命名规则：如果实例化一个，可以为：xxx_u;实例化多个，为：yyy_u0, yyy_u1.
 - 规则3: 信号的命名规则：wire net型全部以 s_xxx 命名
 - 规则4：模块对外接口信号的命名： 输入接口信号为 xxx_i 输出接口信号为 xxx_o
 - 规则5：模块之间点对点接口信号命名规则：s_xxx
 - 规则6: 时钟接口命名规则：如无必要，全部为 clk_i, 如有必要加入频率信息，为clk_freq 如32768， clk_32k768, 128M, clk_128m
 - 规则7: 异步复位接口命名规则：如无必要，全部为 rstn_i
 - 规则8：所有仿真文件命名为 xxx_sim.v 或者 xxx_tb.v
 - 规则9：数（parameter） 常量 （constant）和块标号（block lable）一律采用大写，而信号 变量 结构名 实例标号全部采用小写。
