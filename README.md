# AND-grid
---how to create a test for vhdl
---you can test it with a test bench

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity test_bench is
end test_bench;

architecture Behavioral of test_bench is
    component my_design
        port (
            input1 : in  STD_LOGIC;
            input2 : in  STD_LOGIC;
            output1 : out  STD_LOGIC
        );
    end component;
    signal input1_tb : STD_LOGIC := '0';
    signal input2_tb : STD_LOGIC := '0';
    signal output1_tb : STD_LOGIC;
begin
    dut : my_design port map (
        input1 => input1_tb,
        input2 => input2_tb,
        output1 => output1_tb
    );

    process
    begin
        -- Test case 1: Both inputs are '0'
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 1 failed" severity error;

        -- Test case 2: input1 is '1', input2 is '0'
        input1_tb <= '1';
        wait for 10 ns;
        assert output1_tb = '1' report "Test case 2 failed" severity error;

        -- Test case 3: input1 is '0', input2 is '1'
        input1_tb <= '0';
        input2_tb <= '1';
        wait for 10 ns;
        assert output1_tb = '1' report "Test case 3 failed" severity error;

        -- Test case 4: Both inputs are '1'
        input1_tb <= '1';
        input2_tb <= '1';
        wait for 10 ns;
        assert output1_tb = '1' report "Test case 4 failed" severity error;

        -- Test case 5: input1 is 'Z', input2 is '0'
        input1_tb <= 'Z';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 5 failed" severity error;

        -- Test case 6: input1 is '0', input2 is 'Z'
        input1_tb <= '0';
        input2_tb <= 'Z';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 6 failed" severity error;

        -- Test case 7: Both inputs are 'Z'
        input1_tb <= 'Z';
        input2_tb <= 'Z';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 7 failed" severity error;

        -- Test case 8: input1 is 'X', input2 is '0'
        input1_tb <= 'X';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 8 failed" severity error;

        -- Test case 9: input1 is '0', input2 is 'X'
        input1_tb <= '0';
        input2_tb <= 'X';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 9 failed" severity error;

        -- Test case 10: Both inputs are 'X'
        input1_tb <= 'X';
        input2_tb <= 'X';
        wait for 10 ns;
        assert output1_tb = '0' report "Test case 10 failed" severity error;

        report "All test cases passed" severity note;
        wait;
    end process;
end Behavioral;
