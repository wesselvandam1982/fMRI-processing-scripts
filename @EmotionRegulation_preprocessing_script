#!/bin/tcsh -f

# Sample fMRI preprocessing script using uber_subject.py: version 0.37 (April 14, 2015)
# This script was used to preprocess the fMRI data for an Emotion Regulation study. 

# Input files to this script include anatomical and functional fMRI scans (PS1_s${s}r1.nii,
# PS2_s${s}r1.nii, DS1_s${s}r1.nii, DS2_s${s}r1.nii and s${s}T1.nii) as well as stimulus 
# onset files (${s}.ButtonPress.1D,${s}.instructions_decrease_PS.1D etc.).
# Output files will be moved to a folder called "tshift_outliers_removed_5mm_smoothed_correct_tshift"$s.results

# subjects variable to loop over all participants
set subjects = "1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40"
set study = "ER"


foreach s ( $subjects )

cd $s 

set subj = "tshift_outliers_removed_5mm_smoothed_correct_tshift"$s

afni_proc.py -subj_id $subj                                                 \
        -script proc.$subj -scr_overwrite                                   \
        -blocks despike tshift align tlrc volreg blur mask scale regress    \
        -copy_anat s${s}T1.nii                                \
        -dsets                                               \
            PS1_s${s}r1.nii                                   \
            PS2_s${s}r2.nii                                   \
            DS1_s${s}r3.nii                                   \
            DS2_s${s}r4.nii                                   \
        -tcat_remove_first_trs 4                             \
        -volreg_align_to last                                \
	    -tshift_align_to -tzero 0                            \
        -volreg_no_extent_mask                               \
        -tlrc_opts_at -pad_base 60                           \
       -volreg_align_e2a                                     \
        -volreg_tlrc_warp                                    \
		-align_opts_aea -giant_move -resample off            \
        -blur_size 5.0 						                 \
	-blur_in_automask                                        \
	-test_stim_files no                                      \
        -regress_stim_times                                  \
            ${s}.ButtonPress.1D                              \
            ${s}.instructions_decrease_PS.1D                    \
            ${s}.instructions_decrease_DS.1D                    \
            ${s}.instructions_look_PS.1D                        \
            ${s}.instructions_look_DS.1D                        \
            ${s}.instructions_neutral.1D                     \
            ${s}.negative_decrease_PS.1D                        \
            ${s}.negative_decrease_DS.1D                        \
            ${s}.negative_look_PS.1D                            \
            ${s}.negative_look_DS.1D                            \
            ${s}.neutral_look_PS.1D                             \
            ${s}.neutral_look_DS.1D                             \
            ${s}.NULL.1D                                     \
            ${s}.positive_decrease_PS.1D                        \
            ${s}.positive_decrease_DS.1D                        \
            ${s}.positive_look_PS.1D                            \
            ${s}.positive_look_DS.1D                            \
        -regress_stim_labels                                 \
            	BP InstDec_PS InstDec_DS InstLook_PS InstLook_DS InstNeu \
            	NegDec_PS NegDec_DS NegLook_PS NegLook_DS \
            	NeuLook_PS NeuLook_DS NULL \
            	PosDec_PS PosDec_DS PosLook_PS PosLook_DS \
       -regress_basis_multi 						         \
		'WAV(1)' 'WAV(3)' 'WAV(3)' 'WAV(3)' 'WAV(3)' 'WAV(3)'  \
                 'WAV(6)' 'WAV(6)' 'WAV(6)' 'WAV(6)'           \
                 'WAV(6)' 'WAV(6)' 'WAV(3)'                  \
                 'WAV(6)' 'WAV(6)' 'WAV(6)' 'WAV(6)'         \
		-regress_stim_types times times times times times times    \
	  		                times times times times                \
				            times times times                \
				            times times times times          \
	-regress_apply_mot_types demean deriv   			     \
	-mask_segment_anat yes						             \
	-regress_ROI CSFe						                 \
        -regress_censor_motion 1.3                           \
	    -regress_censor_prev no                              \
	-regress_censor_outliers 0.25					         \
        -regress_est_blur_errts						         \
	-regress_run_clustsim no					             \
	-regress_make_cbucket yes                                \
	-regress_opts_3dD						                 \
	-num_glt 11   \
		-gltsym 'SYM: +InstDec_PS -InstDec_DS -InstLook_PS +InstLook_DS' \
		-glt_label 1 DecLookxPreDur \
                -gltsym 'SYM: InstDec_PS -InstLook_PS' \
                -glt_label 2 InstDec_PS-InstLook_PS \
                -gltsym 'SYM: InstDec_DS -InstLook_DS' \
                -glt_label 3 InstDec_DS-InstLook_DS \
                -gltsym 'SYM: +NegDec_PS -NegDec_DS -NegLook_PS +NegLook_DS' \
                -glt_label 4 NegDecLookxPreDur \
                -gltsym 'SYM: +PosDec_PS -PosDec_DS -PosLook_PS +PosLook_DS' \
                -glt_label 5 PosDecLookxPreDur \
                -gltsym 'SYM: NegDec_PS -NegLook_PS' \
                -glt_label 6 NegDec_PS-NegLook_PS \
                -gltsym 'SYM: NegDec_DS -NegLook_DS' \
                -glt_label 7 NegDec_DS-NegLook_DS \
                -gltsym 'SYM: PosDec_PS -PosLook_PS' \
                -glt_label 8 NegDec_PS-NegLook_PS \
                -gltsym 'SYM: PosDec_DS -PosLook_DS' \
                -glt_label 9 PosDec_DS-PosLook_DS \
                -gltsym 'SYM: NeuLook_PS -NeuLook_DS' \
                -glt_label 10 NeuLook_PS-NeuLook_DS \
                -gltsym 'SYM: BP -NULL' \
                -glt_label 11 BP-NULL \
		-jobs 2 \
		-bucket stats.$subj.wave.24 \
	-write_3dD_prefix basis.wave24 \
	-regress_3dD_stop 	\
	-regress_reml_exec \
	-execute

cd ..
	
end
