Verilog-ML
==========

like HAML but for Verilog.

The intention is to allow very simple templates for use with code generation 


    format = FixedPoint.format(1,8,16)
    verilog Test
      inputs
        clk
        rst_n
        data_rx, format 
      outputs
        data_tx, format

      body

        flop 
          negedge rst_n
            data_tx <= 'b0
          posedge clk
            data_tx <= data_rx



Returns :

    module Test(
      input  clk,
      input  rst_n,
      input  [23:0] data_rx, // SFix(8, 16)
      output [23:0] data_tx  // SFix(8, 16)
    );

    always @(posedge clk or negedge rst_n) begin
      if (rst_n == 1'b0) begin //first statement negedge => 0, posedge => 1
        data_tx <= 'b0 ;
      end
      else begin
        data_tx <= data_rx ;
      end
    end

    endmodule

Or a to_erb version can be used where the Data Format can be supplied as a parameter

* Semicolons added automatically
* Begin,End added based on indentation
* Formats used to comment datatypes
